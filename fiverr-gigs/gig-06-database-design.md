# I will design or optimize your PostgreSQL or MongoDB database schema

---

## Category

**Programming & Tech > Software Development > Database Administration**

---

## Search Keywords (Top 5 Tags)

| # | Tag                      |
|---|--------------------------|
| 1 | `database design`        |
| 2 | `database optimization`  |
| 3 | `sql`                    |
| 4 | `database migration`     |
| 5 | `sequelize`              |

---

## Keyword Research Analysis

- **"database design"** — The single highest-searched database keyword on Fiverr in 2025-2026. Buyers searching this term are at the start of a project and need schema architecture from scratch. It signals high-value, greenfield work and maps directly to the Standard tier.
- **"database optimization"** — The second highest-searched database keyword. These buyers have an existing database that is slow, bloated, or poorly structured. They are in pain and willing to pay a premium for someone who can diagnose and fix performance issues. Maps to the Premium tier.
- **"sql"** — Broad catch-all that captures a massive volume of searches. Many buyers type "sql" when they need anything database-related but lack the vocabulary to be specific. This tag ensures the gig appears in those general searches and funnels them toward the right package.
- **"database migration"** — Targets buyers with existing projects who need to restructure, move between database engines, or upgrade their ORM layer. This is a high-intent keyword because migration implies an active project with a deadline. Growing in 2026 as more teams migrate from NoSQL back to relational databases.
- **"sequelize"** — Niche ORM-specific keyword that most sellers ignore. Developers searching "sequelize" on Fiverr need help with models, associations, migrations, or performance tuning in that specific toolchain. Low competition, high conversion. Directly maps to my Obenan experience with 400+ Sequelize migrations.

**Why these keywords beat alternatives:** The title already contains "design," "optimize," "PostgreSQL," "MongoDB," and "database schema," so tags avoid repeating those words. Instead, tags cover the broader search terms ("sql"), the pain-point search ("database optimization"), the lifecycle search ("database migration"), and the tooling niche ("sequelize") to cast the widest net without keyword overlap.

---

## Pricing Table

| Feature                                       | Basic ($60)        | Standard ($150)         | Premium ($350)                   |
|-----------------------------------------------|--------------------|-------------------------|----------------------------------|
| **Delivery Time**                             | 2 days             | 5 days                  | 7 days                           |
| **Revisions**                                 | 1                  | 2                       | 3                                |
| Schema Review & Audit Report                  | Yes                | Yes                     | Yes                              |
| ER Diagram (Visual Schema Map)                | Yes                | Yes                     | Yes                              |
| Full Schema Design (up to 20 tables/collections) | -               | Yes                     | Yes                              |
| Model Definitions (Sequelize / Mongoose)      | -                  | Yes                     | Yes                              |
| Relationships & Associations                  | -                  | Yes                     | Yes                              |
| Seed Data Scripts                             | -                  | Yes                     | Yes                              |
| Migration Files (versioned, reversible)       | -                  | -                       | Yes                              |
| Query Optimization & Indexing Strategy        | -                  | -                       | Yes                              |
| Multi-Tenant Data Isolation                   | -                  | -                       | Yes                              |
| Performance Benchmarks & Recommendations      | -                  | -                       | Yes                              |
| Documentation (schema dictionary + decisions) | -                  | -                       | Yes                              |

---

## Gig Description

**A bad database schema does not just slow down your queries. It slows down your entire engineering team. I will design a clean, scalable schema or fix the one that is already hurting you.**

I am Saad Sohail, a Senior Full-Stack Engineer with 6+ years of hands-on database architecture experience across PostgreSQL, MongoDB, Redis, and SQL Server. I have designed schemas for multi-tenant SaaS platforms, real estate marketplaces, and AI-powered applications, and I bring that depth of experience to every project.

### What You Get

#### Basic — Schema Review & Audit ($60)

You send me your existing schema or Sequelize/Mongoose models. I deliver a detailed audit report covering:

- Normalization issues and redundant data patterns.
- Missing or misapplied indexes that are causing slow queries.
- Relationship and foreign key problems.
- Naming convention inconsistencies.
- Specific, actionable recommendations ranked by impact.

#### Standard — Full Schema Design ($150)

I design your database from requirements. Deliverables include:

- ER diagram with all entities, relationships, and cardinality.
- Sequelize models (PostgreSQL) or Mongoose schemas (MongoDB) ready to drop into your codebase.
- Properly defined associations (one-to-one, one-to-many, many-to-many with junction tables).
- Seed data scripts for development and testing.
- Index recommendations for your expected query patterns.

#### Premium — Migration, Optimization & Scaling ($350)

Everything in Standard, plus:

- Versioned, reversible migration files that integrate with your deployment pipeline.
- Query analysis using EXPLAIN ANALYZE with targeted index creation.
- Multi-tenant data isolation strategy (row-level security, schema-per-tenant, or shared with tenant_id).
- Performance benchmarks before and after optimization.
- Full schema documentation with a data dictionary and architectural decision records.

### Real Production Experience

- **Obenan** — Architected a multi-tenant SaaS database with **100+ Sequelize models** and **400+ versioned migrations** across PostgreSQL. Designed tenant isolation, complex polymorphic associations, and query patterns that scaled to thousands of businesses without performance degradation.
- **Zamulk** — Built a real estate platform spanning **100+ cities** with PostGIS geospatial indexing for location-based property search. Designed schemas for listings, bidding history, user profiles, and transaction logs with sub-100ms query times on millions of rows.
- **GoTo API** — Designed the data layer for an AI transcription platform using NestJS and PostgreSQL, including schemas for audio processing jobs, transcription results, and billing records.
- **AT-Function-GPT** — Structured the database for a GPT-4o-mini ticket analysis system, handling high-throughput write patterns for real-time ticket classification and reporting.

### Databases & Tools I Work With

**Relational:** PostgreSQL, MySQL, SQL Server.
**Document:** MongoDB, DynamoDB.
**Cache/Queue:** Redis, BullMQ.
**ORMs:** Sequelize, Mongoose, TypeORM, Prisma.
**Design Tools:** dbdiagram.io, pgAdmin, MongoDB Compass, DataGrip.

### Who This Is For

- Founders building an MVP who need a schema that will not collapse when they scale.
- Engineering teams with slow queries, growing tech debt, or migration headaches.
- Developers migrating from MongoDB to PostgreSQL (or vice versa) and need a clean schema translation.
- Anyone who has ever said "we will fix the database later" and now it is later.

**Message me before ordering** with a description of your project, your current database (if any), and the problem you are trying to solve. I will recommend the right package.

---

## FAQ

**Q: Do you work with databases other than PostgreSQL and MongoDB?**
A: Yes. I also work with MySQL, SQL Server, DynamoDB, and Redis. PostgreSQL and MongoDB are listed in the title because they cover the majority of requests, but I am experienced across the full spectrum.

**Q: Can you optimize queries without redesigning the whole schema?**
A: Absolutely. The Basic package includes a query audit with specific index recommendations. In many cases, adding the right composite index or rewriting a single query can cut response times by 90% without touching the schema at all.

**Q: Will you write the migration files, or just give me a diagram?**
A: The Premium package includes fully written, versioned migration files (Sequelize, Knex, or raw SQL) that you can run with a single command. They are reversible, so you can roll back safely if needed.

**Q: How do you handle multi-tenant databases?**
A: I evaluate three strategies based on your scale and compliance needs: shared database with tenant_id column (simplest), schema-per-tenant (moderate isolation), or database-per-tenant (full isolation). I built Obenan's multi-tenant architecture with shared-database row-level isolation across 100+ models.

**Q: Can you help if I am using an ORM I did not mention?**
A: Yes. I have worked with Sequelize, Mongoose, TypeORM, Prisma, and Knex. If you are using a different ORM, message me and I will confirm.

**Q: Do you provide ongoing database support?**
A: This gig covers the initial design, migration, or optimization engagement. For ongoing database maintenance, monitoring, and query tuning, I offer a separate retainer arrangement. Ask me for details after delivery.

---

## Image Guidelines

- **Thumbnail (1280x769):** Clean dark background (charcoal #1E1E2E) with a simplified ER diagram showing 5-6 connected tables. Overlay text: "Database Design -- PostgreSQL -- MongoDB -- 100+ Model Experience." Use the PostgreSQL elephant icon and MongoDB leaf icon side by side.
- **Image 2:** Side-by-side comparison — left panel shows a messy, un-normalized schema with red warning icons, right panel shows the same data cleanly restructured with green checkmarks. Caption: "Before & After Schema Optimization."
- **Image 3:** Screenshot of a real ER diagram from dbdiagram.io showing a subset of a multi-tenant schema (redact sensitive details). Annotate key design decisions with callout arrows.
- **Image 4:** Terminal screenshot showing a Sequelize migration running successfully with timestamps and table creation logs. Caption: "400+ Migrations. Zero Downtime."
- **Image 5:** Performance benchmark chart showing query response times before and after optimization (e.g., "SELECT with JOIN: 2,400ms down to 45ms after indexing"). Use a clean bar chart with red (before) and green (after).
- **General:** Maintain consistent dark theme across all images. Use monospace font (JetBrains Mono or Fira Code) for any code or SQL snippets. Ensure text is readable at mobile thumbnail size.
