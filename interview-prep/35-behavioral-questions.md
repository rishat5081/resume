# 35. BEHAVIORAL & SOFT SKILL QUESTIONS

## 35.1 Common Questions & Answer Frameworks

**Use STAR method: Situation → Task → Action → Result**

### Q: Tell me about yourself
**What:** An open-ended prompt to deliver a concise professional summary covering your experience, current role, and key strengths.
**Why:** Usually the first question asked — a strong answer sets the tone for the entire interview and frames how the interviewer perceives you.

> "I'm a Senior Full-Stack Engineer with 6+ years of experience building production-grade systems. I currently work at Global Software Consulting where I architect AI-powered SaaS platforms using Node.js, PostgreSQL, MongoDB, and AWS. I've integrated LLMs like GPT-4 and Claude into production systems, built RAG architectures, and managed infrastructure serving thousands of businesses. I'm passionate about clean architecture, scalable systems, and shipping quality software."

### Q: Describe a challenging technical problem you solved
**What:** A STAR-format question asking you to walk through a real production problem, your approach, and the measurable outcome.
**Why:** Demonstrates your problem-solving ability, technical depth, and impact — the most important signal interviewers look for in senior engineers.

> **Situation:** At Obenan, we had a SaaS platform serving thousands of businesses, and review fetching from Google was bottlenecking our system.
> **Task:** I needed to process thousands of review fetches without blocking the main application.
> **Action:** I designed an asynchronous job processing pipeline using BullMQ and Redis. Jobs were queued with retry logic, exponential backoff, and concurrency limits. I also added a sentiment analysis step using GPT-4 that ran as a separate job in the pipeline.
> **Result:** Review processing became fully async with zero impact on API response times. The system handled 10x more reviews with automatic retry on failures.

### Q: How do you handle disagreements with team members?
**What:** A question testing your conflict resolution skills and ability to collaborate under differing opinions.
**Why:** Shows you can navigate team dynamics professionally — a critical skill for senior roles where cross-team collaboration is expected.

> Focus on data and outcomes, not opinions. Propose A/B testing or prototyping when possible. Ultimately defer to whoever owns the decision, but ensure concerns are documented.

### Q: How do you stay updated with new technologies?
**What:** A question about your learning habits and how you keep your skills current in a fast-evolving industry.
**Why:** Signals intellectual curiosity and growth mindset — companies want engineers who adapt to new tools and patterns without being pushed.

> I follow tech blogs, participate in open-source, experiment with new tools in side projects, and actively use AI-assisted development (Claude Code, Codex) to explore cutting-edge patterns.

### Q: What's your biggest weakness?
**What:** A self-awareness question where you identify a genuine weakness and show how you actively work to improve it.
**Why:** Tests honesty and self-reflection — interviewers want to see you can identify blind spots and take concrete steps to address them.

> "I sometimes over-engineer solutions — anticipating future requirements that may never come. I've learned to focus on shipping the simplest solution first and iterating based on real user feedback."

### Q: Why should we hire you?
**What:** A closing pitch where you summarize your unique value proposition and what differentiates you from other candidates.
**Why:** Your final chance to leave a strong impression — directly tying your skills to what the company needs shows preparation and confidence.

> "I bring a rare combination of deep backend expertise, hands-on AI/LLM integration experience, and proven ability to architect production systems at scale. I've built systems handling thousands of businesses with multi-tenant isolation, integrated multiple AI providers, and managed full AWS infrastructure. I don't just write code — I design systems that ship, scale, and maintain."

---

# QUICK REFERENCE CHEAT SHEET

## One-Liner Definitions

| Term | Definition |
|------|-----------|
| **REST** | Architectural style using HTTP methods for CRUD on resources |
| **GraphQL** | Query language where clients specify exactly what data they need |
| **JWT** | Encoded token containing user claims, signed with a secret |
| **OAuth** | Authorization protocol — lets apps access user data without passwords |
| **RBAC** | Access control based on user roles (admin, user, viewer) |
| **ACID** | Atomicity, Consistency, Isolation, Durability — DB transaction guarantees |
| **ORM** | Maps database tables to code objects (Sequelize, TypeORM) |
| **Middleware** | Function between request and response that processes/modifies data |
| **WebSocket** | Full-duplex communication channel over a single TCP connection |
| **Redis** | In-memory key-value store for caching, queues, pub/sub |
| **Docker** | Containerization platform — packages app + dependencies together |
| **CI/CD** | Automated build, test, and deployment pipeline |
| **RAG** | Feed retrieved documents to an LLM for accurate, grounded answers |
| **Fine-tuning** | Further training a pre-trained model on your specific data |
| **Embedding** | Converting text to a numerical vector for similarity search |
| **Vector DB** | Database optimized for storing and searching embeddings |
| **Multi-tenant** | Single app serving multiple isolated customers |
| **Microservices** | Architecture where each feature is an independent service |
| **Load Balancer** | Distributes incoming traffic across multiple servers |
| **Reverse Proxy** | Server (Nginx) that forwards requests to backend servers |

---

## Your Resume Projects — Quick Reference for Interviews

| Project | Stack | Key Achievement |
|---------|-------|----------------|
| **Obenan/Global Software Consulting** | Node.js, PostgreSQL, MongoDB, AWS, BullMQ, Stripe | 100+ models, 400+ migrations, multi-tenant SaaS, AI sentiment analysis |
| **GoTo API** | NestJS, TypeScript, Next.js | AI transcription with AWS Transcribe + GPT-4o, webhook processing |
| **AT-Function-GPT** | NestJS, TypeScript, Next.js 14 | Automated ticket analysis with GPT-4o-mini, Azure Key Vault |
| **NowVPlay** | Node.js, MongoDB, Socket.IO, AWS | Real-time sports platform, content moderation, CI/CD |
| **Zamulk** | Node.js, MongoDB, Socket.IO | Real estate portal (100+ cities), geospatial search, live bidding |
| **US Ride** | Node.js, Socket.IO, Stripe | Real-time ride tracking, peer-to-peer payments |

