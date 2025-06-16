# QuizMaster - Technical Documentation

## System Architecture Deep Dive

### Frontend Architecture

#### Component Structure
```
client/src/
├── components/
│   ├── ui/              # Reusable UI components (buttons, inputs, etc.)
│   ├── layout/          # Layout components (header, sidebar, etc.)
│   ├── quiz/            # Quiz-specific components
│   └── auth/            # Authentication components
├── pages/
│   ├── HomePage.tsx     # Landing page
│   ├── QuizPage.tsx     # Quiz interface
│   ├── StatsPage.tsx    # Statistics dashboard
│   └── AuthPage.tsx     # Login/Register
├── hooks/
│   ├── useAuth.ts       # Authentication hook
│   ├── useQuiz.ts       # Quiz state management
│   └── useStats.ts      # Statistics fetching
└── lib/
    ├── api.ts           # API client functions
    ├── utils.ts         # Utility functions
    └── constants.ts     # Application constants
```

#### State Management Strategy
- **Server State**: TanStack Query for API data caching and synchronization
- **Client State**: React Context for global UI state (theme, language)
- **Form State**: React Hook Form for complex form handling
- **Local State**: useState for component-specific state

#### Routing Implementation
```typescript
// Using Wouter for lightweight routing
import { Route, Switch } from 'wouter';

function App() {
  return (
    <Switch>
      <Route path="/" component={HomePage} />
      <Route path="/quiz/:category" component={QuizPage} />
      <Route path="/stats" component={StatsPage} />
      <Route path="/auth" component={AuthPage} />
    </Switch>
  );
}
```

### Backend Architecture

#### Express.js Server Structure
```
server/
├── routes/
│   ├── auth.ts          # Authentication endpoints
│   ├── quiz.ts          # Quiz-related endpoints
│   ├── categories.ts    # Category management
│   └── stats.ts         # Statistics endpoints
├── middleware/
│   ├── auth.ts          # Authentication middleware
│   ├── validation.ts    # Request validation
│   └── error.ts         # Error handling
├── services/
│   ├── authService.ts   # Authentication business logic
│   ├── quizService.ts   # Quiz business logic
│   └── statsService.ts  # Statistics calculations
└── index.ts             # Server entry point
```

#### Database Connection Management
```typescript
// Using Neon Database with connection pooling
import { neon } from '@neondatabase/serverless';
import { drizzle } from 'drizzle-orm/neon-http';

const sql = neon(process.env.DATABASE_URL!);
export const db = drizzle(sql);
```

### Database Design

#### Entity Relationship Diagram
```
Users (1) ──── (N) QuizSessions
  │                    │
  │                    │
  └── (1) ──── (N) UserActivities
  │
  └── (1) ──── (1) UserStats

Categories (1) ──── (N) Questions
     │                    │
     └──────────────────── (N) QuizSessions
```

#### Schema Definitions
```typescript
// User table with authentication and profile data
export const users = pgTable('users', {
  id: uuid('id').primaryKey().defaultRandom(),
  email: text('email').unique().notNull(),
  password: text('password').notNull(),
  username: text('username').unique().notNull(),
  status: text('status').default('offline'),
  createdAt: timestamp('created_at').defaultNow(),
  updatedAt: timestamp('updated_at').defaultNow(),
});

// Categories for organizing quizzes
export const categories = pgTable('categories', {
  id: uuid('id').primaryKey().defaultRandom(),
  name: text('name').notNull(),
  description: text('description'),
  icon: text('icon').notNull(),
  color: text('color').notNull(),
  difficulty: integer('difficulty').default(1),
  isActive: boolean('is_active').default(true),
});

// Questions with multiple choice answers
export const questions = pgTable('questions', {
  id: uuid('id').primaryKey().defaultRandom(),
  categoryId: uuid('category_id').references(() => categories.id),
  question: text('question').notNull(),
  options: json('options').$type<string[]>().notNull(),
  correctAnswer: integer('correct_answer').notNull(),
  explanation: text('explanation'),
  difficulty: integer('difficulty').default(1),
});
```

## API Design Patterns

### RESTful Endpoint Structure
```
GET    /api/categories           # List all categories
GET    /api/categories/:id       # Get specific category
POST   /api/quiz/start           # Start new quiz session
POST   /api/quiz/submit          # Submit quiz answers
GET    /api/quiz/history         # Get user's quiz history
GET    /api/stats/user           # Get user statistics
POST   /api/auth/register        # User registration
POST   /api/auth/login           # User login
POST   /api/auth/logout          # User logout
```

### Request/Response Patterns
```typescript
// Standardized API response format
interface ApiResponse<T> {
  success: boolean;
  data?: T;
  error?: string;
  message?: string;
}

// Quiz submission request
interface QuizSubmissionRequest {
  sessionId: string;
  answers: Array<{
    questionId: string;
    selectedAnswer: number;
    timeSpent: number;
  }>;
  totalTime: number;
}

// Quiz results response
interface QuizResultsResponse {
  score: number;
  totalQuestions: number;
  correctAnswers: number;
  timeSpent: number;
  results: Array<{
    questionId: string;
    correct: boolean;
    explanation?: string;
  }>;
}
```

## Security Implementation

### Authentication Flow
1. **Registration**: Password hashing with bcryptjs (12 rounds)
2. **Login**: Credential verification and session creation
3. **Session Management**: HTTP-only cookies with PostgreSQL store
4. **Logout**: Session destruction and cookie clearing

### Security Middleware
```typescript
// Authentication middleware
export const requireAuth = (req: Request, res: Response, next: NextFunction) => {
  if (!req.session?.userId) {
    return res.status(401).json({ error: 'Authentication required' });
  }
  next();
};

// Input validation middleware
export const validateRequest = (schema: ZodSchema) => {
  return (req: Request, res: Response, next: NextFunction) => {
    try {
      schema.parse(req.body);
      next();
    } catch (error) {
      res.status(400).json({ error: 'Invalid request data' });
    }
  };
};
```

### Data Validation
```typescript
// Zod schemas for request validation
export const registerSchema = z.object({
  email: z.string().email(),
  password: z.string().min(8),
  username: z.string().min(3).max(20),
});

export const quizSubmissionSchema = z.object({
  sessionId: z.string().uuid(),
  answers: z.array(z.object({
    questionId: z.string().uuid(),
    selectedAnswer: z.number().min(0).max(3),
    timeSpent: z.number().positive(),
  })),
  totalTime: z.number().positive(),
});
```

## Performance Optimizations

### Frontend Optimizations
- **Code Splitting**: Route-based lazy loading
- **Memoization**: React.memo for expensive components
- **Virtual Scrolling**: For large question lists
- **Image Optimization**: WebP format with fallbacks

### Backend Optimizations
- **Database Indexing**: Strategic indexes on frequently queried columns
- **Connection Pooling**: Efficient database connection management
- **Caching**: In-memory caching for static data
- **Compression**: Gzip compression for API responses

### Database Query Optimization
```sql
-- Indexes for performance
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_quiz_sessions_user_id ON quiz_sessions(user_id);
CREATE INDEX idx_questions_category_id ON questions(category_id);
CREATE INDEX idx_user_activities_user_id ON user_activities(user_id);

-- Optimized query for user statistics
SELECT 
  u.id,
  u.username,
  COUNT(qs.id) as total_quizzes,
  AVG(qs.score) as average_score,
  MAX(qs.score) as best_score
FROM users u
LEFT JOIN quiz_sessions qs ON u.id = qs.user_id
WHERE u.id = $1
GROUP BY u.id, u.username;
```

## Error Handling Strategy

### Frontend Error Boundaries
```typescript
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    console.error('Error caught by boundary:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <ErrorFallback />;
    }
    return this.props.children;
  }
}
```

### Backend Error Handling
```typescript
// Global error handler
export const errorHandler = (
  err: Error,
  req: Request,
  res: Response,
  next: NextFunction
) => {
  console.error(err.stack);
  
  if (err instanceof ZodError) {
    return res.status(400).json({
      error: 'Validation error',
      details: err.errors
    });
  }
  
  res.status(500).json({
    error: 'Internal server error'
  });
};
```

## Testing Strategy

### Unit Testing Approach
- **Components**: React Testing Library for UI components
- **Hooks**: Custom hook testing with renderHook
- **Services**: Jest for business logic testing
- **API**: Supertest for endpoint testing

### Integration Testing
- **Database**: Test database with seed data
- **Authentication**: End-to-end auth flow testing
- **Quiz Flow**: Complete quiz session testing

## Deployment Configuration

### Environment Variables
```bash
# Database
DATABASE_URL=postgresql://user:password@host:port/database

# Session
SESSION_SECRET=your-secret-key

# Application
NODE_ENV=production
PORT=3000
```

### Docker Configuration
```dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .
RUN npm run build

EXPOSE 3000

CMD ["npm", "start"]
```

## Monitoring and Analytics

### Performance Metrics
- **Response Times**: API endpoint performance tracking
- **Database Queries**: Query execution time monitoring
- **User Engagement**: Quiz completion rates and user activity

### Error Tracking
- **Client Errors**: JavaScript error reporting
- **Server Errors**: Express error logging
- **Database Errors**: Connection and query error tracking

This technical documentation provides a comprehensive overview of the QuizMaster application's architecture, implementation details, and best practices used throughout the development process.