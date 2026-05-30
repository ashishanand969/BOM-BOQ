# 🚀 Setup Guide - BOM-BOQ Calculator

Complete step-by-step guide to set up the Bill of Material and Bill of Quantity Calculator.

## Prerequisites

Before you start, ensure you have the following installed:

- **Node.js** v18.0.0 or higher ([Download](https://nodejs.org/))
- **npm** v9.0.0 or higher (comes with Node.js)
- **PostgreSQL** v12 or higher ([Download](https://www.postgresql.org/))
- **Git** ([Download](https://git-scm.com/))
- **Visual Studio Code** (optional but recommended) ([Download](https://code.visualstudio.com/))

### Verify Installations

```bash
# Check Node.js version
node --version      # Should be v18.0.0 or higher

# Check npm version
npm --version       # Should be v9.0.0 or higher

# Check PostgreSQL version
psql --version      # Should be PostgreSQL 12 or higher

# Check Git version
git --version       # Should be git 2.x or higher
```

## Step 1: Clone the Repository

```bash
# Clone the repository
git clone https://github.com/ashishanand969/BOM-BOQ.git

# Navigate to project directory
cd BOM-BOQ

# View directory structure
ls -la
```

## Step 2: Set Up PostgreSQL Database

### Option A: Using PostgreSQL CLI

```bash
# Access PostgreSQL
psql -U postgres

# Create database
CREATE DATABASE bom_boq;

# Create user with password
CREATE USER bom_user WITH PASSWORD 'your_secure_password';

# Grant privileges
GRANT ALL PRIVILEGES ON DATABASE bom_boq TO bom_user;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT ALL ON TABLES TO bom_user;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT ALL ON SEQUENCES TO bom_user;

# Exit PostgreSQL
\q
```

### Option B: Using PostgreSQL GUI (pgAdmin)

1. Open pgAdmin (usually runs on http://localhost:5050)
2. Right-click on "Databases" → Create → Database
3. Enter name: `bom_boq`
4. Create a new user with credentials
5. Grant all privileges to the user

### Option C: Using Docker (Easiest)

```bash
# Run PostgreSQL in Docker
docker run --name bom-boq-db \
  -e POSTGRES_DB=bom_boq \
  -e POSTGRES_USER=bom_user \
  -e POSTGRES_PASSWORD=your_secure_password \
  -p 5432:5432 \
  -d postgres:15-alpine

# Verify PostgreSQL is running
docker ps
```

## Step 3: Backend Setup

```bash
# Navigate to backend directory
cd backend

# Install dependencies
npm install

# Copy environment template
cp .env.example .env

# Edit .env file with your database credentials
# Update DATABASE_URL with your PostgreSQL connection string
nano .env  # or use your preferred editor
```

### Update .env File

```env
DATABASE_URL="postgresql://bom_user:your_secure_password@localhost:5432/bom_boq?schema=public"
JWT_SECRET="your_super_secret_key_change_in_production"
CORS_ORIGIN="http://localhost:3000"
PORT=5000
NODE_ENV=development
```

### Initialize Database

```bash
# Generate Prisma Client
npm run prisma:generate

# Run database migrations
npm run db:migrate

# Optional: Seed database with sample data
npm run db:seed

# Start backend server
npm run dev
```

**Expected Output:**
```
✔ Server running on http://localhost:5000
✔ Database connected successfully
✔ API documentation available at http://localhost:5000/api/docs
```

## Step 4: Frontend Setup

```bash
# Navigate to frontend directory (from project root)
cd ../frontend

# Install dependencies
npm install

# Copy environment template
cp .env.example .env.local

# Update environment variables (optional - defaults should work)
# nano .env.local
```

### Start Frontend Development Server

```bash
npm run dev
```

**Expected Output:**
```
- Local:        http://localhost:3000
- Environments: .env.local
✔ Ready in XXXms
```

## Step 5: Verify Installation

### Backend Verification

```bash
# Test API health endpoint
curl http://localhost:5000/health

# Expected response:
# {"status":"ok","timestamp":"2026-05-30T..."}
```

### Frontend Verification

- Open http://localhost:3000 in your browser
- You should see the login page
- If you see the page, frontend is working ✓

### Database Verification

```bash
# From backend directory
npx prisma studio

# Opens database UI at http://localhost:5555
```

## Step 6: First Time Setup - Create Admin Account

### Via API

```bash
# Register a new user
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "admin@datoms.io",
    "password": "SecurePassword123!",
    "name": "Admin User"
  }'

# Login with the account
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "admin@datoms.io",
    "password": "SecurePassword123!"
  }'

# You'll receive a JWT token - copy it for API requests
```

### Via Frontend

1. Go to http://localhost:3000
2. Click "Sign Up"
3. Enter your details
4. Complete registration
5. Login with your credentials

## Common Issues & Solutions

### Issue: PostgreSQL Connection Error

**Error:** `error: connect ECONNREFUSED 127.0.0.1:5432`

**Solutions:**
```bash
# Check if PostgreSQL is running
psql -U postgres -c "SELECT 1"

# If not running, start PostgreSQL:
# macOS
brew services start postgresql

# Ubuntu/Debian
sudo systemctl start postgresql

# Windows
net start postgresql-x64-15
```

### Issue: Port Already in Use

**Error:** `Error: listen EADDRINUSE: address already in use :::3000`

**Solutions:**
```bash
# Find process using port 3000
lsof -i :3000  # macOS/Linux
netstat -ano | findstr :3000  # Windows

# Kill the process
kill -9 <PID>  # macOS/Linux
taskkill /PID <PID> /F  # Windows

# Or use a different port
PORT=3001 npm run dev
```

### Issue: Database Migration Failed

**Error:** `Error: P3007 Migration failed`

**Solutions:**
```bash
# Reset database (WARNING: Deletes all data)
npx prisma migrate reset

# Or manually run migrations
npx prisma db push
npx prisma generate
```

### Issue: Node Modules Error

**Error:** `Cannot find module 'xyz'`

**Solutions:**
```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm cache clean --force
npm install
```

### Issue: Environment Variables Not Loaded

**Error:** `Error: DATABASE_URL is not set`

**Solutions:**
```bash
# Verify .env file exists and is in correct directory
ls -la .env

# Check if variable is properly set
cat .env | grep DATABASE_URL

# Reload environment
source .env  # Linux/macOS
# Windows: Just restart the terminal
```

## Development Tools Setup (Optional)

### Install ESLint & Prettier

```bash
# Backend
cd backend
npm install --save-dev eslint prettier eslint-config-prettier eslint-plugin-prettier

# Frontend
cd ../frontend
npm install --save-dev eslint prettier eslint-config-next eslint-plugin-react
```

### Install PostMan for API Testing

1. Download [Postman](https://www.postman.com/downloads/)
2. Import API collection from `docs/postman-collection.json`
3. Set `{{base_url}}` to `http://localhost:5000`
4. Start testing endpoints

## Running in Production Mode

### Build Frontend

```bash
cd frontend
npm run build
npm start
```

### Build Backend

```bash
cd backend
npm run build
npm start
```

## Docker Setup (Alternative)

### Using Docker Compose

```bash
# Build and run all services
docker-compose up --build

# Services will be available at:
# Frontend: http://localhost:3000
# Backend: http://localhost:5000
# PostgreSQL: localhost:5432
```

## Next Steps

1. ✅ **Explore the Dashboard** - Get familiar with the interface
2. ✅ **Create a Test Project** - Try creating your first BOQ/BOM
3. ✅ **Test Exports** - Generate PDF, Excel, and CSV documents
4. ✅ **Read API Documentation** - See `docs/API.md`
5. ✅ **Check Feature Documentation** - See `docs/FEATURES.md`

## Getting Help

- 📖 Check [API Documentation](./API.md)
- 📋 See [Feature Guide](./FEATURES.md)
- 🐛 Report issues on [GitHub Issues](https://github.com/ashishanand969/BOM-BOQ/issues)
- 💌 Contact team at support@datoms.io

---

**Happy coding! 🚀**
