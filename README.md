# 🎮 The Build Log News

> **"Ars Technica meets Digital Foundry for gaming"**  
> A gaming news and analysis platform for technically-minded gamers and developers.

[![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Next.js](https://img.shields.io/badge/Next.js-14-black)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue)](https://www.typescriptlang.org/)
[![NestJS](https://img.shields.io/badge/NestJS-10-red)](https://nestjs.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue)](https://www.postgresql.org/)

---

## 📖 Table of Contents

- [Vision & Mission](#-vision--mission)
- [Tech Stack](#-tech-stack)
- [Architecture](#-architecture)
- [Getting Started](#-getting-started)
- [Project Structure](#-project-structure)
- [Database Schema](#-database-schema)
- [Authentication](#-authentication)
- [Git Workflow](#-git-workflow)
- [Development Roadmap](#-development-roadmap)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Vision & Mission

**The Build Log News** is the most trusted technical publication in gaming journalism. We bridge the gap between game development insights and consumer-facing news.

### What We Deliver

| Content Type | Description |
|--------------|-------------|
| 🔬 **Technical Analysis** | Deep-dives into game engines, graphics pipelines, and performance optimization |
| 📊 **Performance Benchmarks** | Objective metrics, FPS data, load times, and hardware comparisons |
| 🎙️ **Developer Interviews** | Insights from the creators behind your favorite games |
| 📰 **Breaking News** | Coverage of SDKs, APIs, and industry tools |
| 📝 **Community Content** | User-generated guides, modding tutorials, and peer reviews |

### Core Principles

1. **Technical Integrity** — Every claim backed by verifiable data, code samples, or developer insights
2. **Transparent Methodology** — Fully documented review processes and testing setups
3. **Developer-First Approach** — Content for technical audiences who understand gaming at a systems level
4. **Community Collaboration** — Tools for user-generated technical analysis and peer review

---

## 🛠️ Tech Stack

### Frontend
| Technology | Purpose |
|------------|---------|
| **Next.js 14** (App Router) | SSR/SSG, optimal performance, SEO |
| **TypeScript 5.x** | Type safety, better DX |
| **Tailwind CSS 3.x** | Utility-first styling |
| **Shadcn/ui + Radix UI** | Accessible, composable components |
| **TanStack Query v5** | Server state management, caching |
| **Zod** | Runtime type validation |
| **Zustand** | Client state management |

### Backend
| Technology | Purpose |
|------------|---------|
| **NestJS 10** | Modular API structure, maintainability |
| **PostgreSQL 15** | Primary relational database |
| **Prisma ORM** | Type-safe database access, migrations |
| **Redis 7.x** | Caching, sessions, real-time features |
| **MeiliSearch** | Full-text search, typo tolerance |
| **MinIO** | S3-compatible object storage |

### Infrastructure
| Technology | Purpose |
|------------|---------|
| **Docker** | Containerization, local development |
| **GitHub Actions** | CI/CD, automated testing |
| **Vercel / AWS** | Deployment, hosting |
| **Cloudflare** | CDN, DDoS protection |

### Monitoring & Analytics
| Technology | Purpose |
|------------|---------|
| **Sentry** | Error tracking, performance monitoring |
| **PostHog** | Product analytics, user behavior |

---

## 🏗️ Architecture

### Monorepo Structure (pnpm Workspaces)

```
the-build-log-news/
├── apps/
│   ├── web/                    # Next.js 14 frontend
│   │   ├── app/                # App Router pages & layouts
│   │   ├── components/         # React components
│   │   ├── lib/                # Utilities, hooks, API clients
│   │   └── styles/             # Global styles, Tailwind config
│   │
│   ├── api/                    # NestJS backend API
│   │   ├── src/
│   │   │   ├── modules/        # Feature modules
│   │   │   ├── common/         # Shared utilities, guards
│   │   │   └── config/         # Configuration
│   │   └── prisma/             # Database schema & migrations
│   │
│   └── admin/                  # Admin dashboard (future)
│
├── packages/
│   ├── types/                  # Shared TypeScript types
│   ├── utils/                  # Shared utilities
│   ├── ui/                     # Shared UI component library
│   └── config/                 # Shared ESLint, TypeScript configs
│
├── infrastructure/
│   ├── docker/                 # Docker configurations
│   ├── .github/                # GitHub Actions workflows
│   └── scripts/                # Build & deployment scripts
│
├── docs/                       # Documentation
├── docker-compose.yml          # Local development services
├── turbo.json                  # Turborepo configuration
└── pnpm-workspace.yaml         # Workspace configuration
```

### Why Monorepo?

| Benefit | Description |
|---------|-------------|
| ✅ **Shared Types** | Single source of truth for TypeScript interfaces |
| ✅ **Unified Tooling** | Consistent ESLint, Prettier, TypeScript configs |
| ✅ **Atomic Changes** | Frontend + Backend changes in single PR |
| ✅ **Simplified DevEx** | One clone, one install, everything works |
| ✅ **Scalable** | Easy to add admin dashboard, mobile API, etc. |

---

## 🚀 Getting Started

### Prerequisites

- **Node.js 20+** (LTS recommended)
- **pnpm 8+** (package manager)
- **Docker & Docker Compose** (for local services)
- **Git** (version control)

### Quick Start

```bash
# 1. Clone the repository
git clone https://github.com/Abdelhakim-Baalla/The-Build-Log-News.git
cd the-build-log-news

# 2. Install dependencies
pnpm install

# 3. Copy environment files
cp apps/web/.env.example apps/web/.env.local
cp apps/api/.env.example apps/api/.env

# 4. Start infrastructure services
docker compose up -d

# 5. Setup database
pnpm db:push
pnpm db:seed

# 6. Start development servers
pnpm dev
```

### Access Points

| Service | URL |
|---------|-----|
| 🌐 Frontend | http://localhost:3000 |
| 🔌 API | http://localhost:4000/api |
| 📚 API Docs | http://localhost:4000/docs |
| 🔍 MeiliSearch | http://localhost:7700 |
| 📧 Mailpit | http://localhost:8025 |
| 🗄️ Adminer | http://localhost:8080 |

---

## 📁 Project Structure

### Frontend (`apps/web/`)

```
app/
├── (auth)/                 # Auth routes (login, register)
├── (main)/                 # Main layout routes
│   ├── articles/           # Article pages
│   ├── games/              # Game database
│   ├── reviews/            # Review pages
│   └── profile/            # User profile
├── api/                    # API routes (NextAuth, etc.)
├── layout.tsx              # Root layout
└── page.tsx                # Homepage

components/
├── ui/                     # Base UI components (button, card, etc.)
├── layout/                 # Header, Footer, Sidebar
├── articles/               # Article-specific components
├── reviews/                # Review-specific components
└── shared/                 # Shared components

lib/
├── api/                    # API client setup
├── hooks/                  # Custom React hooks
├── utils/                  # Utility functions
└── validations/            # Zod schemas
```

### Backend (`apps/api/`)

```
src/
├── modules/
│   ├── auth/               # Authentication & authorization
│   ├── users/              # User management
│   ├── articles/           # Article CRUD, publishing
│   ├── games/              # Game database
│   ├── reviews/            # Review system
│   ├── comments/           # Comment system
│   └── search/             # MeiliSearch integration
│
├── common/
│   ├── decorators/         # Custom decorators
│   ├── guards/             # Auth guards, RBAC
│   ├── filters/            # Exception filters
│   ├── interceptors/       # Response transformers
│   └── pipes/              # Validation pipes
│
└── config/
    ├── database.config.ts
    ├── auth.config.ts
    └── app.config.ts

prisma/
├── schema.prisma           # Database schema
├── migrations/             # Migration files
└── seed.ts                 # Database seeding
```

---

## 🗄️ Database Schema

### Entity Relationship Overview

```
┌─────────────┐       ┌─────────────┐       ┌─────────────┐
│    User     │───────│   Article   │───────│    Game     │
│  (author)   │ 1:N   │             │ N:M   │             │
└─────────────┘       └─────────────┘       └─────────────┘
       │                     │
       │ 1:N                 │ 1:1
       ▼                     ▼
┌─────────────┐       ┌─────────────┐
│   Comment   │       │   Review    │
│  (nested)   │       │(benchmarks) │
└─────────────┘       └─────────────┘
```

### Core Entities

#### User
| Field | Type | Description |
|-------|------|-------------|
| `id` | UUID | Primary key |
| `email` | String | Unique, verified |
| `username` | String | Unique, display name |
| `role` | Enum | `READER`, `CONTRIBUTOR`, `EDITOR`, `ADMIN` |
| `avatar` | String? | Profile image URL |
| `bio` | Text? | User biography |
| `socialLinks` | JSON | Twitter, GitHub, etc. |
| `reputationScore` | Int | Community contribution score |

#### Article
| Field | Type | Description |
|-------|------|-------------|
| `id` | UUID | Primary key |
| `slug` | String | Unique, SEO-friendly URL |
| `title` | String | Article title |
| `excerpt` | String | Short summary |
| `content` | JSON | Rich text content (blocks) |
| `type` | Enum | `NEWS`, `REVIEW`, `ANALYSIS`, `GUIDE`, `OPINION` |
| `status` | Enum | `DRAFT`, `REVIEW`, `PUBLISHED`, `ARCHIVED` |
| `authorId` | UUID | Foreign key to User |
| `featuredImage` | String? | Hero image URL |
| `tags` | String[] | Keywords, categories |
| `metadata` | JSON | Read time, word count, etc. |
| `publishedAt` | DateTime? | Publication date |

#### Game
| Field | Type | Description |
|-------|------|-------------|
| `id` | UUID | Primary key |
| `slug` | String | Unique identifier |
| `title` | String | Game name |
| `developer` | String | Development studio |
| `publisher` | String | Publishing company |
| `releaseDate` | DateTime | Release date |
| `platforms` | String[] | PC, PS5, Xbox, Switch, etc. |
| `genres` | String[] | FPS, RPG, Strategy, etc. |
| `engine` | String? | Unreal, Unity, etc. |
| `technicalSpecs` | JSON | System requirements, APIs |

#### Review
| Field | Type | Description |
|-------|------|-------------|
| `id` | UUID | Primary key |
| `articleId` | UUID | Foreign key to Article |
| `overallScore` | Float | 1-10 rating |
| `scores` | JSON | Graphics, performance, gameplay, etc. |
| `pros` | String[] | Positive points |
| `cons` | String[] | Negative points |
| `benchmarks` | JSON | FPS data, load times, hardware tests |
| `verdict` | Text | Final summary |

#### Comment
| Field | Type | Description |
|-------|------|-------------|
| `id` | UUID | Primary key |
| `content` | Text | Comment body |
| `authorId` | UUID | Foreign key to User |
| `articleId` | UUID | Foreign key to Article |
| `parentId` | UUID? | For nested comments |
| `upvotes` | Int | Vote count |
| `isEdited` | Boolean | Edit flag |

---

## 🔐 Authentication

### Strategy Overview

| Method | Provider | Use Case |
|--------|----------|----------|
| 📧 Email/Password | NextAuth | Traditional registration |
| 🐙 GitHub OAuth | NextAuth | Developer accounts |
| 🔵 Google OAuth | NextAuth | General users |
| 🟣 Discord OAuth | NextAuth | Gaming community |

### Role-Based Access Control (RBAC)

```
ADMIN ────────────────────────────────────────────────────►
  ├── Full system access
  ├── User management
  └── Site configuration

EDITOR ───────────────────────────────────────────►
  ├── Publish/unpublish articles
  ├── Moderate comments
  └── Manage game database

CONTRIBUTOR ─────────────────────────────►
  ├── Write articles (requires review)
  ├── Submit reviews
  └── Enhanced commenting

READER ────────────────────────►
  ├── Read all content
  ├── Comment on articles
  └── Vote on comments
```

### JWT Token Flow

```
1. User logs in → Server validates credentials
2. Server generates:
   - Access Token (15 min expiry)
   - Refresh Token (7 day expiry, stored in httpOnly cookie)
3. Client uses Access Token for API requests
4. On expiry, Refresh Token obtains new Access Token
```

---

## 🔄 Git Workflow

### Branch Strategy (Git Flow Lite)

```
main ─────────────────────────────────────────────────►
  │                                    │
  │   ┌──► release/v1.0 ──────────────▲│
  │   │                                │
develop ────┼────────────────────────────────────────►
  │         │
  ├── feature/user-auth ──────►
  ├── feature/article-editor ──────►
  └── hotfix/login-bug (→ main + develop)
```

### Branch Naming Convention

| Type | Pattern | Example |
|------|---------|---------|
| Feature | `feature/<description>` | `feature/user-authentication` |
| Bugfix | `fix/<issue-id>-<description>` | `fix/123-login-redirect` |
| Hotfix | `hotfix/<description>` | `hotfix/security-patch` |
| Release | `release/v<version>` | `release/v1.0.0` |
| Docs | `docs/<description>` | `docs/api-documentation` |

### Commit Convention (Conventional Commits)

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

| Type | Description |
|------|-------------|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation |
| `style` | Formatting (no code change) |
| `refactor` | Code restructuring |
| `perf` | Performance improvement |
| `test` | Adding/updating tests |
| `chore` | Maintenance tasks |
| `ci` | CI/CD changes |

**Examples:**
```bash
feat(auth): add Discord OAuth provider
fix(articles): resolve slug generation conflict
docs(readme): update installation instructions
refactor(api): extract validation logic to pipe
```

### Workflow Commands

```bash
# Start new feature
git checkout develop
git pull origin develop
git checkout -b feature/my-feature

# Regular commits
git add .
git commit -m "feat(scope): description"

# Push and create PR
git push origin feature/my-feature
# Create PR to develop via GitHub

# After PR merged, clean up
git checkout develop
git pull origin develop
git branch -d feature/my-feature
```

---

## 📊 Development Roadmap

### Phase 1: Foundation (Weeks 1-4) 🏗️

- [x] Project architecture decisions
- [x] README documentation
- [ ] Monorepo setup with Turborepo
- [ ] Docker Compose for local development
- [ ] CI/CD pipeline (GitHub Actions)
- [ ] Base TypeScript/ESLint/Prettier configuration
- [ ] Database schema design (Prisma)
- [ ] Authentication system (NextAuth.js)

### Phase 2: Core Features (Weeks 5-8) ⚡

- [ ] User registration & profiles
- [ ] Article CRUD & publishing workflow
- [ ] Rich text editor integration
- [ ] Game database with technical specs
- [ ] Search functionality (MeiliSearch)
- [ ] Homepage & article pages
- [ ] Responsive design implementation

### Phase 3: Reviews & Community (Weeks 9-12) 🎯

- [ ] Review system with benchmark data
- [ ] Comment system with threading
- [ ] Voting & reputation system
- [ ] User dashboards
- [ ] Email notifications
- [ ] SEO optimization

### Phase 4: Polish & Launch (Weeks 13-16) 🚀

- [ ] Performance optimization
- [ ] Security audit
- [ ] Production deployment
- [ ] Monitoring & analytics setup
- [ ] Documentation finalization
- [ ] Beta testing & feedback

---

## 👥 Contributing

We welcome contributions! Please read our guidelines before submitting.

### Quick Steps

1. **Fork** the repository
2. **Clone** your fork locally
3. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
4. **Commit** your changes (following commit conventions)
5. **Push** to your branch (`git push origin feature/amazing-feature`)
6. **Open** a Pull Request to `develop`

### Pull Request Checklist

- [ ] Code follows project style guidelines
- [ ] Tests pass locally (`pnpm test`)
- [ ] Lint passes (`pnpm lint`)
- [ ] TypeScript compiles (`pnpm type-check`)
- [ ] Documentation updated if needed
- [ ] PR description explains changes

### Development Commands

```bash
pnpm dev          # Start all development servers
pnpm build        # Build all packages
pnpm test         # Run all tests
pnpm lint         # Lint all packages
pnpm type-check   # TypeScript validation
pnpm db:push      # Push schema to database
pnpm db:studio    # Open Prisma Studio
```

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 🤝 Support & Contact

| Channel | Link |
|---------|------|
| 🐛 Issues | [GitHub Issues](https://github.com/Abdelhakim-Baalla/The-Build-Log-News/issues) |
| 💬 Discussions | [GitHub Discussions](https://github.com/Abdelhakim-Baalla/The-Build-Log-News/discussions) |
| 📚 Wiki | [Project Wiki](https://github.com/Abdelhakim-Baalla/The-Build-Log-News/wiki) |

---

<div align="center">

**Built with ❤️ for the gaming developer community**

*The Build Log News Team*

</div>