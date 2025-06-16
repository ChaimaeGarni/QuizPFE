# QuizMaster - Interactive Knowledge Platform

## Overview

QuizMaster is a full-stack interactive quiz application built with a modern TypeScript tech stack. The application provides a gamified learning experience with user authentication, categorized quizzes, real-time statistics tracking, and multilingual support. Users can test their knowledge across various subjects, track their progress, and compete with personalized scoring systems.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter for client-side routing
- **State Management**: TanStack Query for server state and React Context for client state
- **UI Components**: Radix UI primitives with custom shadcn/ui components
- **Styling**: Tailwind CSS with CSS variables for theming
- **Build Tool**: Vite with hot module replacement

### Backend Architecture
- **Framework**: Express.js with TypeScript
- **Database**: PostgreSQL with Drizzle ORM
- **Authentication**: Session-based auth with express-session
- **Password Security**: bcryptjs for hashing
- **Database Provider**: Neon Database (@neondatabase/serverless)

### Database Schema
The application uses a relational PostgreSQL schema with the following key entities:
- **Users**: Authentication and profile management with status tracking
- **Categories**: Quiz subject categories with metadata (icon, color, difficulty)
- **Questions**: Multiple-choice questions with explanations and difficulty levels
- **Quiz Sessions**: Complete quiz attempts with scoring and timing
- **User Activities**: Activity logging for engagement tracking
- **User Stats**: Aggregated performance statistics

## Key Components

### Authentication System
- Session-based authentication with secure HTTP-only cookies
- User registration and login with input validation using Zod schemas
- Password hashing with bcryptjs
- Protected routes middleware for API endpoints
- User status management (online, idle, dnd, offline)

### Quiz Engine
- Dynamic question loading by category
- Timed quiz sessions with configurable duration
- Real-time scoring and progress tracking
- Multiple choice question format with explanations
- Difficulty progression system

### User Interface
- Responsive design with mobile-first approach
- Dark/light theme support with system preference detection
- Multilingual support (English, Spanish, French, German, Chinese)
- Animated transitions and micro-interactions
- Accessible components following WCAG guidelines

### Statistics Dashboard
- Real-time performance metrics
- Activity timeline tracking
- Category-wise performance analysis
- Achievement and progress visualization

## Data Flow

1. **Authentication Flow**: User credentials → Session validation → Protected route access
2. **Quiz Flow**: Category selection → Question loading → Answer submission → Score calculation → Results display
3. **Statistics Flow**: Quiz completion → Activity logging → Statistics aggregation → Dashboard updates
4. **Theme Flow**: User preference → Local storage → CSS variable updates → Component re-rendering

## External Dependencies

### Frontend Dependencies
- **@tanstack/react-query**: Server state management and caching
- **@radix-ui/react-***: Accessible UI component primitives
- **wouter**: Lightweight client-side routing
- **react-hook-form**: Form state management with validation
- **@hookform/resolvers**: Form validation resolvers
- **zod**: TypeScript-first schema validation
- **tailwindcss**: Utility-first CSS framework
- **class-variance-authority**: Type-safe variant styling

### Backend Dependencies
- **drizzle-orm**: Type-safe SQL query builder
- **@neondatabase/serverless**: Serverless PostgreSQL driver
- **express-session**: Session management middleware
- **bcryptjs**: Password hashing utility
- **connect-pg-simple**: PostgreSQL session store
- **zod**: Schema validation for API endpoints

### Development Dependencies
- **vite**: Fast build tool and dev server
- **typescript**: Type safety and enhanced development experience
- **tsx**: TypeScript execution for development
- **esbuild**: Fast JavaScript bundler for production builds

## Deployment Strategy

### Development Environment
- **Runtime**: Node.js 20 with ESM modules
- **Database**: PostgreSQL 16 with automatic provisioning
- **Development Server**: Vite dev server with HMR on port 5000
- **Session Storage**: PostgreSQL-backed session store

### Production Build
- **Frontend**: Vite build with optimized bundle splitting
- **Backend**: esbuild compilation to ESM format
- **Static Assets**: Served from `/dist/public` directory
- **Database Migrations**: Drizzle Kit for schema management

### Replit Configuration
- **Modules**: nodejs-20, web, postgresql-16
- **Deployment**: Autoscale deployment target (full-stack Express.js app)
- **Build Command**: npm run build (builds both frontend with Vite and backend with esbuild)
- **Run Command**: npm start (starts production Express server)
- **Port Configuration**: Internal port 5000 mapped to external port 80
- **Environment Variables**: DATABASE_URL for PostgreSQL connection

## Changelog

```
Changelog:
- June 14, 2025. Initial setup
```

## User Preferences

```
Preferred communication style: Simple, everyday language.
```