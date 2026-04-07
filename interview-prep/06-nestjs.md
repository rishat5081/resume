# 6. NESTJS

## 6.1 What is NestJS?
NestJS is an **opinionated, Angular-inspired Node.js framework** built with TypeScript. It uses decorators, dependency injection, and a modular architecture.

## 6.2 Core Architecture

```
┌─────────────────────────────────────┐
│              Module                   │
│  ┌─────────┐ ┌──────────┐ ┌──────┐ │
│  │Controller│ │  Service  │ │Guard │ │
│  │(Routes)  │→│(Business  │ │(Auth)│ │
│  │          │ │ Logic)    │ │      │ │
│  └─────────┘ └──────────┘ └──────┘ │
│              ┌──────────┐           │
│              │   Pipe    │           │
│              │(Validate) │           │
│              └──────────┘           │
└─────────────────────────────────────┘
```

### Module
**What:** The organizational building block of a NestJS app that groups related controllers, services, and imports into a cohesive unit with explicit dependency boundaries.
**Why:** Interviewers ask about modules to see if you understand NestJS's modular architecture and how it enforces separation of concerns at scale.

```typescript
@Module({
  imports: [DatabaseModule, AuthModule],
  controllers: [UsersController],
  providers: [UsersService],
  exports: [UsersService], // Make available to other modules
})
export class UsersModule {}
```

### Controller
**What:** A class decorated with `@Controller()` that handles incoming HTTP requests, delegates business logic to services, and returns responses.
**Why:** Controllers are the entry point for every request in NestJS -- interviewers test whether you understand how decorators like `@Get`, `@Post`, and parameter decorators wire up routing.

```typescript
@Controller('users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {} // DI

  @Get()
  findAll(@Query('page') page: number) {
    return this.usersService.findAll(page);
  }

  @Get(':id')
  findOne(@Param('id', ParseIntPipe) id: number) {
    return this.usersService.findOne(id);
  }

  @Post()
  @UseGuards(AuthGuard)
  create(@Body() createUserDto: CreateUserDto) {
    return this.usersService.create(createUserDto);
  }
}
```

### Service
**What:** An `@Injectable()` class that encapsulates business logic and data access, injected into controllers (or other services) via NestJS's dependency injection container.
**Why:** Services demonstrate your understanding of the single-responsibility principle and DI -- two concepts interviewers consider essential for scalable backend design.

```typescript
@Injectable()
export class UsersService {
  constructor(
    @InjectRepository(User)
    private usersRepo: Repository<User>,
  ) {}

  async findAll(page: number): Promise<User[]> {
    return this.usersRepo.find({
      skip: (page - 1) * 10,
      take: 10,
    });
  }

  async findOne(id: number): Promise<User> {
    const user = await this.usersRepo.findOne({ where: { id } });
    if (!user) throw new NotFoundException(`User #${id} not found`);
    return user;
  }
}
```

### Guards (Authentication)
**What:** Classes implementing `CanActivate` that run before route handlers to determine whether a request should be allowed (e.g., JWT verification, role checks).
**Why:** Guards are how NestJS handles auth declaratively -- interviewers ask about them to see if you know how to protect routes without cluttering controller logic.

```typescript
@Injectable()
export class JwtAuthGuard implements CanActivate {
  canActivate(context: ExecutionContext): boolean {
    const request = context.switchToHttp().getRequest();
    const token = request.headers.authorization?.split(' ')[1];
    if (!token) throw new UnauthorizedException();

    try {
      const payload = jwt.verify(token, SECRET);
      request.user = payload;
      return true;
    } catch {
      throw new UnauthorizedException();
    }
  }
}
```

### Pipes (Validation)
**What:** Transform-and-validate layers that process incoming data before it reaches the route handler, typically using DTOs with `class-validator` decorators.
**Why:** Interviewers test pipes to see if you validate input at the framework level rather than scattering manual checks throughout your business logic.

```typescript
// DTO with class-validator
export class CreateUserDto {
  @IsString()
  @MinLength(2)
  name: string;

  @IsEmail()
  email: string;

  @IsStrongPassword()
  password: string;
}

// NestJS automatically validates using the DTO
@Post()
@UsePipes(new ValidationPipe({ whitelist: true }))
create(@Body() dto: CreateUserDto) { }
```

