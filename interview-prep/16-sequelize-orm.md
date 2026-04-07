# 16. SEQUELIZE ORM

## 16.1 What is Sequelize?
Sequelize is a **Promise-based Node.js ORM** for SQL databases (PostgreSQL, MySQL, SQLite, MSSQL). You used it at Obenan with 100+ models and 400+ migrations.

## 16.2 Core Concepts

### Model Definition
**What:** A Sequelize model maps a JavaScript class to a database table, defining columns, types, validations, and indexes.
**Why:** Interviewers test whether you can design schema-level constraints and understand how ORM models translate to actual SQL tables.

```javascript
const { DataTypes } = require('sequelize');

module.exports = (sequelize) => {
  const User = sequelize.define('User', {
    id: {
      type: DataTypes.UUID,
      defaultValue: DataTypes.UUIDV4,
      primaryKey: true,
    },
    name: {
      type: DataTypes.STRING(100),
      allowNull: false,
      validate: { len: [2, 100] },
    },
    email: {
      type: DataTypes.STRING,
      unique: true,
      validate: { isEmail: true },
    },
    role: {
      type: DataTypes.ENUM('user', 'admin', 'superadmin'),
      defaultValue: 'user',
    },
    metadata: {
      type: DataTypes.JSONB, // PostgreSQL
    },
  }, {
    tableName: 'users',
    timestamps: true,      // createdAt, updatedAt
    paranoid: true,        // soft delete (deletedAt)
    indexes: [
      { fields: ['email'], unique: true },
      { fields: ['role'] },
    ],
  });

  return User;
};
```

### Associations
**What:** Associations define relationships between models (one-to-one, one-to-many, many-to-many) that Sequelize uses to generate JOINs and foreign keys.
**Why:** Every backend interview expects you to explain table relationships and how eager/lazy loading affects query performance.

```javascript
// One-to-Many
User.hasMany(Post, { foreignKey: 'userId', as: 'posts' });
Post.belongsTo(User, { foreignKey: 'userId', as: 'author' });

// Many-to-Many
User.belongsToMany(Role, { through: 'user_roles' });
Role.belongsToMany(User, { through: 'user_roles' });

// One-to-One
User.hasOne(Profile, { foreignKey: 'userId' });
Profile.belongsTo(User, { foreignKey: 'userId' });
```

### Queries
**What:** Sequelize provides methods like findOne, findAll, findAndCountAll, and raw queries for reading and manipulating data with built-in pagination, filtering, and eager loading.
**Why:** Interviewers want to see that you can write efficient ORM queries, know when to use raw SQL, and understand how transactions ensure data consistency.

```javascript
// Find with associations (eager loading)
const user = await User.findOne({
  where: { id: userId },
  include: [
    { model: Post, as: 'posts', where: { status: 'published' }, required: false },
    { model: Profile, as: 'profile' }
  ],
  attributes: ['id', 'name', 'email'],
});

// Pagination
const { count, rows } = await User.findAndCountAll({
  where: { role: 'admin' },
  limit: 10,
  offset: (page - 1) * 10,
  order: [['createdAt', 'DESC']],
});

// Raw query (when ORM is too limiting)
const results = await sequelize.query(
  'SELECT * FROM users WHERE age > :age',
  { replacements: { age: 25 }, type: QueryTypes.SELECT }
);

// Transactions
const t = await sequelize.transaction();
try {
  await User.create({ name: 'Saad' }, { transaction: t });
  await Profile.create({ userId: user.id }, { transaction: t });
  await t.commit();
} catch (error) {
  await t.rollback();
}
```

### Migrations
**What:** Migrations are version-controlled scripts that apply incremental schema changes (create tables, add columns, add indexes) to the database.
**Why:** Production databases can't be wiped and recreated, so interviewers ask how you safely evolve schemas without data loss using up/down migrations.

```javascript
// npx sequelize migration:generate --name add-users-table
module.exports = {
  up: async (queryInterface, Sequelize) => {
    await queryInterface.createTable('users', {
      id: { type: Sequelize.UUID, primaryKey: true },
      name: { type: Sequelize.STRING, allowNull: false },
      email: { type: Sequelize.STRING, unique: true },
      createdAt: { type: Sequelize.DATE },
      updatedAt: { type: Sequelize.DATE },
    });
    await queryInterface.addIndex('users', ['email']);
  },
  down: async (queryInterface) => {
    await queryInterface.dropTable('users');
  },
};
```

### Multi-Tenant Scoping (Your Obenan Experience)
**What:** Multi-tenant scoping ensures every database query is filtered by a tenant identifier (companyId, locationId) so users only see their own data.
**Why:** Data isolation is a critical SaaS concern, and interviewers ask about it to verify you can prevent cross-tenant data leaks at the query level.

```javascript
// Scope queries by company, user, and location
const reviews = await Review.findAll({
  where: {
    companyId: req.user.companyId,    // Tenant isolation
    locationId: req.params.locationId, // Location scoping
  },
  include: [{ model: Location, where: { companyId: req.user.companyId } }],
});
```

