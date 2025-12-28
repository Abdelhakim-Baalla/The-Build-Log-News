# 🎮 The Build Log News – Gaming News & Analysis Platform

> **Authoritative news, reviews, and analysis from the core of gaming and technology.**
> A modern, developer-minded platform for gamers who care about the details behind their games.

[![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Next.js](https://img.shields.io/badge/Next.js-14-black)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue)](https://www.typescriptlang.org/)

## 🎯 Vision & Mission
**The Build Log News** aims to become the most trusted technical publication in gaming journalism. We bridge the gap between game development insights and consumer-facing news, providing:
- **Deep-Dive Technical Analysis** of game engines, graphics, and performance
- **Developer-Focused News** covering SDKs, APIs, and industry tools
- **Comprehensive Reviews** with technical benchmarks and objective metrics
- **Community-Driven Content** from developers, modders, and technical gamers

### Core Principles
1. **Technical Integrity**: Every claim is backed by verifiable data, code samples, or developer insights
2. **Transparent Methodology**: Review processes and testing setups are fully documented
3. **Developer-First Approach**: Content is created for technical audiences who understand gaming at a systems level
4. **Community Collaboration**: Tools for user-generated technical analysis and peer review

## 🏗️ System Architecture (Initial Proposal)
```
The Build Log News Platform
├── frontend/           # Next.js 14 application (App Router)
│   ├── app/           # Page routes & layouts
│   ├── components/    # Reusable React components
│   ├── lib/          # Utilities, hooks, API clients
│   └── styles/       # Tailwind CSS configurations
├── backend/           # API server (NestJS/Express)
│   ├── src/
│   │   ├── modules/  # Feature modules (articles, users, reviews)
│   │   ├── common/   # Shared utilities, guards, filters
│   │   └── config/   # Configuration files
├── shared/            # Shared TypeScript types, interfaces
├── infrastructure/    # Docker, CI/CD, deployment configs
├── docs/             # Project documentation
└── packages/         # Potential monorepo packages
    ├── ui-kit/       # Shared component library
    └── analytics/    # Analytics and tracking utilities
```

## 🛠️ Tech Stack
| Layer | Technology | Purpose | Status |
|-------|------------|---------|--------|
| **Frontend** | Next.js 14 (App Router) | SSR/SSG, optimal performance | ✅ Selected |
| | TypeScript 5.x | Type safety, better developer experience | ✅ Selected |
| | Tailwind CSS 3.x | Utility-first styling, design system | ✅ Selected |
| | Shadcn/ui + Radix UI | Accessible, composable UI components | ✅ Selected |
| | TanStack Query v5 | Server state management, caching | ✅ Selected |
| | Zod | Runtime type validation, schema definition | ✅ Selected |
| **Backend** | NestJS / Express | API structure, maintainability | 🔄 Deciding |
| | PostgreSQL 15 | Primary relational database | ✅ Selected |
| | Prisma ORM | Type-safe database access, migrations | 🔄 Deciding |
| | Redis 7.x | Caching, session storage, real-time features | ✅ Selected |
| | MeiliSearch | Full-text search, typo tolerance, fast queries | ✅ Selected |
| **Infrastructure** | Docker & Docker Compose | Containerization, local development | ✅ Selected |
| | GitHub Actions | CI/CD, automated testing | ✅ Selected |
| | Vercel / AWS | Deployment, hosting, serverless functions | 🔄 Deciding |
| | Cloudflare | CDN, DDoS protection, security | ✅ Selected |
| **Monitoring** | Sentry | Error tracking, performance monitoring | ✅ Selected |
| | PostHog | Product analytics, user behavior | ✅ Selected |

## 🚀 Getting Started

### Prerequisites
- Node.js 18+ and npm/yarn/pnpm
- Docker and Docker Compose (for local database/Redis)
- Git and GitHub account

### Local Development Setup
1. **Clone the repository**
   ```bash
   git clone https://github.com/Abdelhakim-Baalla/the-build-log-news.git
   cd the-build-log-news
   ```

2. **Environment configuration**
   ```bash
   cp .env.example .env.local
   # Edit .env.local with your local values
   ```

3. **Start infrastructure services**
   ```bash
   docker-compose up -d postgres redis meilisearch
   ```

4. **Install dependencies**
   ```bash
   # Using pnpm (recommended)
   pnpm install
   # Or npm
   npm install
   ```

5. **Database setup**
   ```bash
   pnpm db:push    # Push schema to database
   pnpm db:seed    # Seed with initial data
   ```

6. **Run development servers**
   ```bash
   # Start frontend and backend concurrently
   pnpm dev
   # Or separately
   pnpm dev:frontend
   pnpm dev:backend
   ```

7. **Access the application**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:4000/api
   - Database GUI (optional): http://localhost:8080 (Adminer)

## 📁 Project Structure Details

### Frontend Architecture
The frontend follows Next.js 14 App Router conventions with:
- **App Router**: File-based routing with `app/` directory
- **Server Components by default**: Maximize performance, reduce client bundle
- **Parallel & Intercepting Routes**: Advanced routing patterns
- **Streaming**: Progressive content loading with Suspense boundaries

### Backend Architecture
The backend follows a modular, maintainable structure:
- **Clean Architecture/DDD**: Separation of concerns, business logic isolation
- **Repository Pattern**: Abstract data access layer
- **Dependency Injection**: Testable, maintainable code
- **Event-Driven**: Asynchronous processing via message queues

### Database Schema (Key Entities)
```
User
├── id (UUID)
├── email (unique)
├── username (unique)
├── role (USER | EDITOR | ADMIN)
├── profile (JSON: bio, social links, preferences)
└── reputationScore (for community contributions)

Article
├── id (UUID)
├── slug (unique, SEO-friendly)
├── title
├── content (JSON structured content)
├── excerpt
├── type (NEWS | REVIEW | ANALYSIS | OPINION | GUIDE)
├── status (DRAFT | UNDER_REVIEW | PUBLISHED | ARCHIVED)
├── metadata (JSON: readTime, wordCount, featuredImage)
├── gameAssociations (M2M to Game entity)
├── tags (array of keywords)
├── authorId (User relation)
└── technicalDetails (JSON: testedHardware, benchmarks, versionInfo)

Game
├── id (UUID)
├── slug (unique)
├── title
├── developer
├── publisher
├── releaseDate
├── platforms (array)
├── metadata (JSON: genres, ESRB, links to stores)
└── technicalSpecs (JSON: engines, APIs, requirements)

Review
├── id (UUID)
├── articleId (relation to Article)
├── scores (JSON: overall, graphics, performance, gameplay, sound)
├── pros (array)
├── cons (array)
├── benchmarks (JSON: FPS data, load times, hardware tests)
└── editorVerification (boolean: verified purchase/copy)
```

## 🔄 Git Workflow & Branch Strategy

We follow a structured branching model:

### Branch Types
1. **`main`** - Production-ready code only
2. **`develop`** - Integration branch for features
3. **`feature/*`** - New features (e.g., `feature/user-authentication`)
4. **`hotfix/*`** - Critical production fixes
5. **`release/*`** - Release preparation branches

### Workflow Example
```bash
# Start a new feature
git checkout develop
git pull origin develop
git checkout -b feature/article-editor

# Work on feature, commit regularly
git add .
git commit -m "feat(editor): add rich text toolbar"

# Push to remote
git push origin feature/article-editor

# Create PR to develop when ready
```

## 📊 Development Roadmap

### Phase 1: MVP (Months 1-3)
- [ ] **Core Infrastructure**: Project setup, CI/CD, basic architecture
- [ ] **Authentication**: User registration/login with email/password + OAuth
- [ ] **Content Management**: Basic article creation, editing, publishing
- [ ] **Frontend Foundation**: Homepage, article pages, responsive design
- [ ] **Database Schema**: Complete initial schema with all core entities

### Phase 2: Core Features (Months 4-6)
- [ ] **Advanced CMS**: WYSIWYG editor, media management, scheduling
- [ ] **Review System**: Scoring templates, benchmark data visualization
- [ ] **Search & Discovery**: Full-text search, filters, recommendations
- [ ] **Commenting System**: Nested comments, voting, moderation tools
- [ ] **User Profiles**: Dashboards, reading history, preferences

### Phase 3: Advanced Features (Months 7-9)
- [ ] **Community Features**: User-generated guides, peer review system
- [ ] **Technical Analysis Tools**: Benchmark comparison, hardware database
- [ ] **API Platform**: Public REST/GraphQL API for third-party developers
- [ ] **Real-time Features**: Live updates, notifications, websockets
- [ ] **Monetization**: Subscription tiers, premium content, ad integration

## 👥 Contributing

We welcome contributions from the community. Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Commit Convention
We follow [Conventional Commits](https://www.conventionalcommits.org/):
- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `style:` Code style changes (formatting, etc.)
- `refactor:` Code refactoring
- `test:` Adding or updating tests
- `chore:` Maintenance tasks

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Support & Contact
- **Project Issues**: [GitHub Issues](https://github.com/[YOUR-USERNAME]/the-build-log-news/issues)
- **Discussion Forum**: [GitHub Discussions](https://github.com/[YOUR-USERNAME]/the-build-log-news/discussions)
- **Documentation**: [Project Wiki](https://github.com/[YOUR-USERNAME]/the-build-log-news/wiki)

---

**Built with ❤️ for the gaming developer community.**  
*The Build Log News Team*