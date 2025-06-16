# QuizMaster - Project Structure Documentation

## Complete File Structure

```
QuizMaster/
├── 📁 client/                          # Frontend React Application
│   ├── 📄 index.html                   # HTML entry point
│   ├── 📁 src/
│   │   ├── 📄 main.tsx                 # React application entry
│   │   ├── 📄 App.tsx                  # Main App component
│   │   ├── 📄 index.css                # Global styles with Tailwind
│   │   ├── 📁 components/              # Reusable UI Components
│   │   │   ├── 📁 ui/                  # shadcn/ui components
│   │   │   │   ├── 📄 button.tsx       # Button component
│   │   │   │   ├── 📄 card.tsx         # Card component
│   │   │   │   ├── 📄 input.tsx        # Input component
│   │   │   │   ├── 📄 dialog.tsx       # Modal dialog
│   │   │   │   ├── 📄 progress.tsx     # Progress bar
│   │   │   │   └── 📄 ...              # Other UI primitives
│   │   │   ├── 📁 layout/              # Layout Components
│   │   │   │   ├── 📄 Header.tsx       # Application header
│   │   │   │   ├── 📄 Sidebar.tsx      # Navigation sidebar
│   │   │   │   ├── 📄 Footer.tsx       # Application footer
│   │   │   │   └── 📄 Layout.tsx       # Main layout wrapper
│   │   │   ├── 📁 auth/                # Authentication Components
│   │   │   │   ├── 📄 LoginForm.tsx    # Login form
│   │   │   │   ├── 📄 RegisterForm.tsx # Registration form
│   │   │   │   └── 📄 AuthGuard.tsx    # Route protection
│   │   │   ├── 📁 quiz/                # Quiz-Related Components
│   │   │   │   ├── 📄 QuizCard.tsx     # Quiz category card
│   │   │   │   ├── 📄 Question.tsx     # Individual question
│   │   │   │   ├── 📄 QuizTimer.tsx    # Quiz countdown timer
│   │   │   │   ├── 📄 Results.tsx      # Quiz results display
│   │   │   │   └── 📄 Progress.tsx     # Quiz progress indicator
│   │   │   ├── 📁 stats/               # Statistics Components
│   │   │   │   ├── 📄 StatsCard.tsx    # Statistics card
│   │   │   │   ├── 📄 Chart.tsx        # Performance charts
│   │   │   │   └── 📄 Activity.tsx     # Activity timeline
│   │   │   └── 📁 common/              # Common Components
│   │   │       ├── 📄 Loading.tsx      # Loading spinner
│   │   │       ├── 📄 ErrorBoundary.tsx # Error handling
│   │   │       └── 📄 ThemeToggle.tsx  # Theme switcher
│   │   ├── 📁 pages/                   # Application Pages
│   │   │   ├── 📄 HomePage.tsx         # Landing page
│   │   │   ├── 📄 QuizPage.tsx         # Quiz interface
│   │   │   ├── 📄 StatsPage.tsx        # Statistics dashboard
│   │   │   ├── 📄 ProfilePage.tsx      # User profile
│   │   │   ├── 📄 AuthPage.tsx         # Login/Register page
│   │   │   └── 📄 NotFoundPage.tsx     # 404 error page
│   │   ├── 📁 hooks/                   # Custom React Hooks
│   │   │   ├── 📄 useAuth.ts           # Authentication hook
│   │   │   ├── 📄 useQuiz.ts           # Quiz state management
│   │   │   ├── 📄 useStats.ts          # Statistics fetching
│   │   │   ├── 📄 useTheme.ts          # Theme management
│   │   │   └── 📄 useLocalStorage.ts   # Local storage hook
│   │   ├── 📁 lib/                     # Utility Libraries
│   │   │   ├── 📄 api.ts               # API client functions
│   │   │   ├── 📄 utils.ts             # General utilities
│   │   │   ├── 📄 constants.ts         # Application constants
│   │   │   ├── 📄 validations.ts       # Form validation schemas
│   │   │   └── 📄 types.ts             # TypeScript type definitions
│   │   ├── 📁 contexts/                # React Contexts
│   │   │   ├── 📄 AuthContext.tsx      # Authentication context
│   │   │   ├── 📄 ThemeContext.tsx     # Theme context
│   │   │   └── 📄 LanguageContext.tsx  # Internationalization
│   │   └── 📁 assets/                  # Static Assets
│   │       ├── 📁 images/              # Image files
│   │       ├── 📁 icons/               # Icon files
│   │       └── 📁 fonts/               # Custom fonts
│   └── 📄 vite-env.d.ts                # Vite type definitions
├── 📁 server/                          # Backend Express Application
│   ├── 📄 index.ts                     # Server entry point
│   ├── 📁 routes/                      # API Route Handlers
│   │   ├── 📄 auth.ts                  # Authentication endpoints
│   │   ├── 📄 quiz.ts                  # Quiz-related endpoints
│   │   ├── 📄 categories.ts            # Category management
│   │   ├── 📄 questions.ts             # Question management
│   │   ├── 📄 stats.ts                 # Statistics endpoints
│   │   └── 📄 users.ts                 # User management
│   ├── 📁 middleware/                  # Express Middleware
│   │   ├── 📄 auth.ts                  # Authentication middleware
│   │   ├── 📄 validation.ts            # Request validation
│   │   ├── 📄 cors.ts                  # CORS configuration
│   │   ├── 📄 session.ts               # Session management
│   │   └── 📄 error.ts                 # Error handling
│   ├── 📁 services/                    # Business Logic Services
│   │   ├── 📄 authService.ts           # Authentication logic
│   │   ├── 📄 quizService.ts           # Quiz business logic
│   │   ├── 📄 statsService.ts          # Statistics calculations
│   │   ├── 📄 userService.ts           # User management
│   │   └── 📄 emailService.ts          # Email notifications
│   ├── 📁 utils/                       # Server Utilities
│   │   ├── 📄 database.ts              # Database connection
│   │   ├── 📄 logger.ts                # Logging utility
│   │   ├── 📄 encryption.ts            # Password hashing
│   │   └── 📄 validators.ts            # Data validation
│   └── 📁 config/                      # Configuration Files
│       ├── 📄 database.ts              # Database configuration
│       ├── 📄 session.ts               # Session configuration
│       └── 📄 environment.ts           # Environment variables
├── 📁 shared/                          # Shared Code (Client & Server)
│   ├── 📄 schema.ts                    # Database schema definitions
│   ├── 📄 types.ts                     # Shared TypeScript types
│   ├── 📄 constants.ts                 # Shared constants
│   └── 📄 validations.ts               # Shared validation schemas
├── 📁 migrations/                      # Database Migration Files
│   ├── 📄 0001_create_users.sql        # User table creation
│   ├── 📄 0002_create_categories.sql   # Categories table
│   ├── 📄 0003_create_questions.sql    # Questions table
│   ├── 📄 0004_create_quiz_sessions.sql # Quiz sessions table
│   ├── 📄 0005_create_user_stats.sql   # User statistics table
│   └── 📄 0006_create_activities.sql   # User activities table
├── 📁 dist/                            # Production Build Output
│   ├── 📁 public/                      # Built frontend assets
│   └── 📄 index.js                     # Built server code
├── 📁 export-package/                  # Project Export for Submission
│   ├── 📄 README.md                    # Project documentation
│   ├── 📄 TECHNICAL_DOCUMENTATION.md  # Technical details
│   └── 📄 PROJECT_STRUCTURE.md        # This file
├── 📄 package.json                     # Project dependencies
├── 📄 package-lock.json                # Dependency lock file
├── 📄 tsconfig.json                    # TypeScript configuration
├── 📄 vite.config.ts                   # Vite build configuration
├── 📄 tailwind.config.ts               # Tailwind CSS configuration
├── 📄 postcss.config.js                # PostCSS configuration
├── 📄 drizzle.config.ts                # Database ORM configuration
├── 📄 components.json                  # shadcn/ui configuration
├── 📄 .replit                          # Replit configuration
├── 📄 replit.md                        # Replit documentation
├── 📄 .gitignore                       # Git ignore rules
└── 📄 README.md                        # Main project README
```

## Key Directory Explanations

### 📁 client/src/components/
Contains all reusable React components organized by functionality:
- **ui/**: Low-level UI primitives (buttons, inputs, cards)
- **layout/**: Page layout components (header, sidebar, footer)
- **auth/**: Authentication-related components
- **quiz/**: Quiz-specific components (questions, timer, results)
- **stats/**: Statistics and analytics components
- **common/**: Shared utility components

### 📁 server/routes/
API endpoint definitions following RESTful conventions:
- **auth.ts**: `/api/auth/*` - Authentication endpoints
- **quiz.ts**: `/api/quiz/*` - Quiz management endpoints
- **categories.ts**: `/api/categories/*` - Category endpoints
- **stats.ts**: `/api/stats/*` - Statistics endpoints

### 📁 server/middleware/
Express middleware for cross-cutting concerns:
- **auth.ts**: Authentication and authorization
- **validation.ts**: Request data validation
- **cors.ts**: Cross-origin resource sharing
- **session.ts**: Session management
- **error.ts**: Global error handling

### 📁 server/services/
Business logic layer separating concerns from routes:
- **authService.ts**: User authentication logic
- **quizService.ts**: Quiz creation and management
- **statsService.ts**: Statistics calculation and aggregation
- **userService.ts**: User profile management

### 📁 shared/
Code shared between client and server:
- **schema.ts**: Drizzle ORM database schema
- **types.ts**: TypeScript interface definitions
- **constants.ts**: Application-wide constants
- **validations.ts**: Zod validation schemas

### 📁 migrations/
Database migration files for schema evolution:
- Sequential SQL files for database changes
- Each migration is atomic and reversible
- Follows naming convention: `NNNN_description.sql`

## File Naming Conventions

### React Components
- **PascalCase**: `QuizCard.tsx`, `LoginForm.tsx`
- **Descriptive names**: Components clearly indicate their purpose
- **Single responsibility**: Each component has one clear function

### Hooks
- **camelCase with 'use' prefix**: `useAuth.ts`, `useQuiz.ts`
- **Custom hooks**: Encapsulate reusable stateful logic
- **Return objects**: Consistent return patterns for hooks

### Services
- **camelCase with 'Service' suffix**: `authService.ts`, `quizService.ts`
- **Business logic**: Pure functions for data manipulation
- **Database interactions**: Centralized data access patterns

### Types and Interfaces
- **PascalCase**: `User`, `QuizSession`, `ApiResponse`
- **Descriptive**: Names clearly indicate data structure
- **Shared**: Common types used across client and server

## Import/Export Patterns

### Barrel Exports
```typescript
// components/index.ts
export { Button } from './ui/button';
export { Card } from './ui/card';
export { QuizCard } from './quiz/QuizCard';
export { LoginForm } from './auth/LoginForm';
```

### Named Exports
```typescript
// services/authService.ts
export const login = async (credentials: LoginCredentials) => { ... };
export const register = async (userData: RegisterData) => { ... };
export const logout = async () => { ... };
```

### Default Exports for Components
```typescript
// components/quiz/QuizCard.tsx
const QuizCard: React.FC<QuizCardProps> = ({ ... }) => { ... };
export default QuizCard;
```

## Configuration Files

### TypeScript Configuration
- **tsconfig.json**: Compiler options and path mapping
- **Strict mode**: Enabled for type safety
- **Path aliases**: `@/` for client, `@shared/` for shared code

### Build Configuration
- **vite.config.ts**: Frontend build and development server
- **drizzle.config.ts**: Database ORM configuration
- **tailwind.config.ts**: CSS framework configuration

### Development Configuration
- **.replit**: Replit platform configuration
- **package.json**: Dependencies and scripts
- **.gitignore**: Version control exclusions

This structure promotes:
- **Separation of concerns**: Clear boundaries between different parts
- **Scalability**: Easy to add new features and components
- **Maintainability**: Logical organization for easy navigation
- **Reusability**: Shared components and utilities
- **Type safety**: TypeScript throughout the application