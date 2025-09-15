# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

### Primary Commands
- `bun run dev` - Start all development servers in parallel
- `bun run dev:web` - Start development server excluding Stripe (recommended for local development)
- `bun run build` - Build all applications and packages
- `bun run typecheck` - Run TypeScript type checking across all packages
- `bun run lint` - Lint all packages and check dependency consistency
- `bun run lint:fix` - Auto-fix linting issues
- `bun run format` - Check code formatting
- `bun run format:fix` - Auto-fix formatting issues

### Database Commands
- `bun db:push` - Push schema changes to database (run from packages/db/ directory or use root command)

### Package Management
- `bun install` - Install all dependencies (uses Bun as package manager)
- `bun run clean` - Clean node_modules
- `bun run clean:workspaces` - Clean all workspace build artifacts

## Architecture Overview

This is a Next.js SaaS boilerplate built as a Turborepo monorepo with the following key architectural decisions:

### Monorepo Structure
- **apps/nextjs/** - Main Next.js application with App Router
- **apps/auth-proxy/** - Authentication proxy service
- **packages/** - Shared packages and utilities
- **tooling/** - Development tooling configurations

### Key Packages
- **@saasfly/api** - tRPC API layer with routers for auth, customer, k8s, stripe, health checks
- **@saasfly/auth** - Authentication utilities (supports both Clerk and NextAuth)
- **@saasfly/db** - Database layer using Kysely for type-safe SQL queries and Prisma for schema management
- **@saasfly/stripe** - Stripe payment processing integration
- **@saasfly/ui** - Shared UI components built with shadcn/ui, Tailwind CSS, and Framer Motion
- **@saasfly/common** - Shared utilities, email templates, and configurations

### Technology Stack
- **Frontend**: Next.js 14 with App Router, React 18, TypeScript
- **Styling**: Tailwind CSS with shadcn/ui components
- **State Management**: Zustand, TanStack Query for server state
- **Database**: PostgreSQL with Kysely (type-safe queries) and Prisma (schema management)
- **Authentication**: Clerk (primary) with NextAuth.js fallback support
- **Payments**: Stripe integration
- **API**: tRPC for end-to-end type safety
- **Monorepo**: Turborepo with Bun package manager
- **Animation**: Framer Motion
- **Content**: Contentlayer2 for MDX processing

### Development Patterns
- Type-safe API calls using tRPC
- Shared workspace packages with `workspace:*` dependencies
- Environment variables managed via `.env.local` files
- Database schema changes via Prisma with Kysely for queries
- Component development using shadcn/ui patterns
- Internationalization support with multiple language files

### Authentication Notes
- Default authentication provider is Clerk (as of June 2025)
- NextAuth implementation available on `feature-nextauth` branch
- Admin access controlled via `ADMIN_EMAIL` environment variable

### Key Directories in Main App
- **src/app/[lang]/** - Internationalized routing structure
- **src/components/** - React components organized by feature
- **src/config/** - Configuration files including i18n, pricing, site settings
- **src/content/** - MDX content for docs and blog
- **src/trpc/** - tRPC client and server setup

### Environment Setup
- Requires PostgreSQL database (local or Vercel Postgres)
- Copy `.env.example` to `.env.local` and configure
- Run `bun db:push` to initialize database schema