# 5. EXPRESS.JS

## 5.1 What is Express.js?
Express is a **minimal, unopinionated web framework** for Node.js. It provides routing, middleware, and HTTP utilities.

## 5.2 Core Concepts

### Middleware Chain
**What:** A sequence of functions that execute in order on every request, each able to read/modify the request and response objects before calling `next()`.
**Why:** Middleware is the core architectural concept of Express -- interviewers expect you to explain how authentication, logging, error handling, and body parsing all hook into the request pipeline.

```javascript
const express = require('express');
const app = express();

// Middleware executes in order
app.use(express.json());                    // 1. Parse JSON body
app.use(cors());                            // 2. Enable CORS
app.use(morgan('dev'));                     // 3. Log requests
app.use('/api', authMiddleware);            // 4. Authenticate /api routes

// Custom middleware
function authMiddleware(req, res, next) {
  const token = req.headers.authorization;
  if (!token) return res.status(401).json({ error: 'No token' });

  try {
    const decoded = jwt.verify(token, SECRET);
    req.user = decoded;
    next(); // Pass to next middleware/route
  } catch (err) {
    res.status(401).json({ error: 'Invalid token' });
  }
}

// Error-handling middleware (4 params)
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Something went wrong' });
});
```

### Routing
**What:** The mechanism that maps HTTP methods and URL paths to specific handler functions, supporting route parameters, query strings, and modular router groups.
**Why:** Interviewers ask about routing to see if you can design clean RESTful APIs and understand how Express matches incoming requests to the correct handler.

```javascript
const router = express.Router();

router.get('/users', getUsers);
router.get('/users/:id', getUserById);
router.post('/users', validateBody, createUser);
router.put('/users/:id', updateUser);
router.delete('/users/:id', deleteUser);

// Route parameters
router.get('/users/:userId/posts/:postId', (req, res) => {
  const { userId, postId } = req.params;
});

// Query parameters: GET /users?page=1&limit=10
router.get('/users', (req, res) => {
  const { page = 1, limit = 10 } = req.query;
});

app.use('/api/v1', router);
```

