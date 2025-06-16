# QuizMaster - Setup and Installation Guide

## Prerequisites

Before setting up the QuizMaster application, ensure you have the following installed:

### Required Software
- **Node.js**: Version 20.x or higher
  - Download from: https://nodejs.org/
  - Verify installation: `node --version`
- **npm**: Comes with Node.js (version 10.x or higher)
  - Verify installation: `npm --version`
- **PostgreSQL**: Version 16.x or higher
  - Download from: https://postgresql.org/download/
  - Alternative: Use cloud PostgreSQL (Neon, Supabase, etc.)

### Optional Tools
- **Git**: For version control
- **VS Code**: Recommended IDE with extensions:
  - TypeScript and JavaScript Language Features
  - Tailwind CSS IntelliSense
  - ES7+ React/Redux/React-Native snippets
  - Prettier - Code formatter

## Installation Steps

### 1. Clone or Download the Project
```bash
# If using Git
git clone <repository-url>
cd QuizMaster

# Or extract from ZIP file
unzip QuizMaster.zip
cd QuizMaster
```

### 2. Install Dependencies
```bash
# Install all project dependencies
npm install

# This will install both frontend and backend dependencies
# The process may take 2-3 minutes depending on your internet connection
```

### 3. Environment Configuration

Create a `.env` file in the root directory:
```bash
# Copy the example environment file
cp .env.example .env
```

Edit the `.env` file with your configuration:
```env
# Database Configuration
DATABASE_URL=postgresql://username:password@localhost:5432/quizmaster

# Session Configuration
SESSION_SECRET=your-super-secret-session-key-here

# Application Configuration
NODE_ENV=development
PORT=5000

# Optional: Email Configuration (for future features)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password
```

### 4. Database Setup

#### Option A: Local PostgreSQL
```bash
# Create database
createdb quizmaster

# Or using psql
psql -U postgres
CREATE DATABASE quizmaster;
\q
```

#### Option B: Cloud Database (Recommended)
1. **Neon Database** (Free tier available):
   - Visit: https://neon.tech/
   - Create account and new project
   - Copy connection string to `DATABASE_URL`

2. **Supabase** (Alternative):
   - Visit: https://supabase.com/
   - Create project and get connection string

### 5. Database Migration
```bash
# Run database migrations to create tables
npm run db:push

# This will create all necessary tables:
# - users
# - categories
# - questions
# - quiz_sessions
# - user_activities
# - user_stats
```

### 6. Seed Database (Optional)
```bash
# Add sample data for testing
npm run db:seed

# This adds:
# - Sample quiz categories
# - Sample questions for each category
# - Test user accounts
```

## Running the Application

### Development Mode
```bash
# Start the development server
npm run dev

# This will:
# - Start the Express.js backend on port 5000
# - Start the Vite frontend dev server
# - Enable hot module replacement
# - Open browser automatically
```

The application will be available at:
- **Frontend**: http://localhost:5000
- **Backend API**: http://localhost:5000/api

### Production Mode
```bash
# Build the application
npm run build

# Start production server
npm start
```

## Verification Steps

### 1. Check Database Connection
```bash
# Test database connectivity
npm run db:check
```

### 2. Verify API Endpoints
Open your browser and test these endpoints:
- http://localhost:5000/api/categories (should return quiz categories)
- http://localhost:5000/api/health (should return server status)

### 3. Test User Registration
1. Navigate to http://localhost:5000
2. Click "Sign Up" or "Register"
3. Create a test account
4. Verify login functionality

### 4. Test Quiz Functionality
1. Log in with your test account
2. Select a quiz category
3. Complete a sample quiz
4. Check statistics page

## Troubleshooting

### Common Issues and Solutions

#### 1. Database Connection Error
```
Error: connect ECONNREFUSED 127.0.0.1:5432
```
**Solution**:
- Ensure PostgreSQL is running
- Check DATABASE_URL in .env file
- Verify database credentials

#### 2. Port Already in Use
```
Error: listen EADDRINUSE: address already in use :::5000
```
**Solution**:
```bash
# Kill process using port 5000
lsof -ti:5000 | xargs kill -9

# Or change port in .env file
PORT=3000
```

#### 3. Module Not Found Errors
```
Error: Cannot find module '@/components/...'
```
**Solution**:
```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

#### 4. TypeScript Compilation Errors
```bash
# Check TypeScript configuration
npm run check

# Fix common issues
npm run lint:fix
```

#### 5. Database Migration Fails
```bash
# Reset database and re-run migrations
npm run db:reset
npm run db:push
```

### Environment-Specific Issues

#### Windows Users
```bash
# If you encounter permission issues
npm config set script-shell "C:\\Program Files\\git\\bin\\bash.exe"

# Or use PowerShell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

#### macOS Users
```bash
# If you encounter permission issues
sudo chown -R $(whoami) ~/.npm
```

#### Linux Users
```bash
# Install build essentials if needed
sudo apt-get install build-essential

# For Ubuntu/Debian
sudo apt-get update
sudo apt-get install nodejs npm postgresql postgresql-contrib
```

## Development Workflow

### 1. Making Changes
```bash
# Create feature branch
git checkout -b feature/new-feature

# Make your changes
# Test locally
npm run dev

# Run type checking
npm run check

# Commit changes
git add .
git commit -m "Add new feature"
```

### 2. Database Changes
```bash
# After modifying schema.ts
npm run db:push

# Generate new migration (if needed)
npm run db:generate
```

### 3. Adding New Dependencies
```bash
# Frontend dependencies
npm install package-name

# Development dependencies
npm install -D package-name

# Update package.json and commit
```

## Performance Optimization

### Development Tips
- Use React DevTools for component debugging
- Enable TypeScript strict mode for better error catching
- Use browser DevTools for network and performance analysis

### Production Optimization
```bash
# Analyze bundle size
npm run build:analyze

# Optimize images and assets
npm run optimize:assets

# Enable compression
npm run build:compress
```

## Security Considerations

### Environment Variables
- Never commit `.env` files to version control
- Use strong, unique SESSION_SECRET
- Rotate secrets regularly in production

### Database Security
- Use connection pooling in production
- Enable SSL for database connections
- Regular backup procedures

### Application Security
- Keep dependencies updated: `npm audit fix`
- Use HTTPS in production
- Implement rate limiting for API endpoints

## Deployment Options

### 1. Replit (Recommended for Students)
- Fork the project on Replit
- Environment variables are managed in Secrets tab
- Automatic deployment on code changes

### 2. Vercel + Railway
- Frontend: Deploy to Vercel
- Backend + Database: Deploy to Railway
- Environment variables in platform settings

### 3. Traditional VPS
- Use PM2 for process management
- Nginx for reverse proxy
- SSL certificates with Let's Encrypt

## Support and Resources

### Documentation
- **React**: https://react.dev/
- **Express.js**: https://expressjs.com/
- **Drizzle ORM**: https://orm.drizzle.team/
- **Tailwind CSS**: https://tailwindcss.com/

### Community
- **Stack Overflow**: Tag questions with relevant technologies
- **GitHub Issues**: Report bugs or request features
- **Discord/Slack**: Join development communities

### Learning Resources
- **TypeScript Handbook**: https://www.typescriptlang.org/docs/
- **React Patterns**: https://reactpatterns.com/
- **Node.js Best Practices**: https://github.com/goldbergyoni/nodebestpractices

---

**Note**: If you encounter any issues not covered in this guide, please check the project's issue tracker or create a new issue with detailed error messages and system information.