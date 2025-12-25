# Installation & Setup Guide

Complete guide to set up Edulume locally for development.

## Prerequisites

- **Node.js**: v20.12.2 or higher
- **Python**: 3.11 or higher
- **MongoDB**: Local or Atlas cloud instance
- **Git**: For version control
- **npm** or **yarn**: Package managers

## Project Structure

```
edulume/
├── client/                 # React frontend
├── server/                 # Express.js backend
├── python-backend/         # FastAPI AI backend
└── README.md
```

## 1. Frontend Setup (React + Vite)

### Installation

```bash
cd client
npm install
```

### Environment Configuration

Create `.env` file in `client/` directory:

```env
# Development
VITE_API_URL=http://localhost:3001/api
VITE_SOCKET_URL=http://localhost:3001
VITE_PYTHON_API_URL=http://localhost:8000

# Production (set in Vercel)
# VITE_API_URL=https://your-server.fly.dev/api
# VITE_SOCKET_URL=https://your-server.fly.dev
# VITE_PYTHON_API_URL=https://your-python-backend.fly.dev
```

### Running Development Server

```bash
npm run dev
```

The frontend will be available at `http://localhost:5173`

### Building for Production

```bash
npm run build
npm run preview
```

### Linting

```bash
npm run lint
```

## 2. Backend Setup (Express.js + Prisma)

### Installation

```bash
cd server
npm install
```

### Database Setup

#### Option A: MongoDB Atlas (Cloud)

1. Create account at https://www.mongodb.com/cloud/atlas
2. Create a cluster
3. Get connection string
4. Update `DATABASE_URL` in `.env`

#### Option B: Local MongoDB

```bash
# Install MongoDB locally
# macOS with Homebrew
brew tap mongodb/brew
brew install mongodb-community

# Start MongoDB
brew services start mongodb-community

# Connection string
mongodb://localhost:27017/edulume
```

### Environment Configuration

Create `.env` file in `server/` directory:

```env
# Database
DATABASE_URL=mongodb+srv://username:password@cluster.mongodb.net/edulume?retryWrites=true&w=majority

# JWT
JWT_SECRET=your_super_secret_jwt_key_here_change_this_in_production

# Email Configuration (Gmail)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password  # Use Gmail App Password, not regular password
FROM_EMAIL=your-email@gmail.com
FROM_NAME=Edulume

# OTP Configuration
OTP_MODE=development  # Set to 'production' to enable OTP verification

# File Storage (R2/Cloudinary)
R2_ACCOUNT_ID=your_r2_account_id
R2_ACCESS_KEY_ID=your_r2_access_key
R2_SECRET_ACCESS_KEY=your_r2_secret_key
R2_UPLOAD_URL_ID=your_r2_upload_url_id
IMGBB_API_KEY=your_imgbb_api_key

# Port
PORT=3001

# Client Configuration
CLIENT_ORIGIN=http://localhost:5173
CLIENT_URL=http://localhost:5173

# AI/ML Services
GROQ_API_KEY=your_groq_api_key

# Admin Configuration
ADMIN_EMAILS=admin@example.com,admin2@example.com

# Python Backend
PYTHON_API_URL=http://localhost:8000

# Redis (Optional - for caching)
REDIS_URL=redis://default:password@host:port

# Google OAuth
GOOGLE_CLIENT_ID=your_google_client_id.apps.googleusercontent.com
GOOGLE_CLIENT_SECRET=your_google_client_secret
GOOGLE_CALLBACK_URL=http://localhost:3001/api/auth/google/callback
```

### Setting Up Gmail App Password

1. Enable 2-Factor Authentication on your Google account
2. Go to https://myaccount.google.com/apppasswords
3. Select "Mail" and "Windows Computer"
4. Generate app password
5. Use this password in `SMTP_PASS`

### Prisma Setup

```bash
# Generate Prisma client
npm run db:generate

# Push schema to database
npm run db:push

# Open Prisma Studio (optional - visual database browser)
npm run db:studio
```

### Running Development Server

```bash
npm run dev
```

The backend will be available at `http://localhost:3001`

### Health Check

```bash
curl http://localhost:3001/api/health
```

## 3. Python Backend Setup (FastAPI)

### Installation

```bash
cd python-backend
python -m venv venv

# Activate virtual environment
# macOS/Linux
source venv/bin/activate

# Windows
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Environment Configuration

Create `.env` file in `python-backend/` directory:

```env
# AI/ML Services
OPENAI_API_KEY=your_openai_api_key
GROQ_API_KEY=your_groq_api_key

# Vector Database (Pinecone)
PINECONE_API_KEY=your_pinecone_api_key
PINECONE_ENVIRONMENT=us-east-1
PINECONE_INDEX_NAME=rag-model

# File Storage (Cloudinary)
CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret

# CORS
ALLOWED_ORIGINS=http://localhost:3000,http://localhost:5173,http://localhost:3001
```

### Getting API Keys

#### OpenAI API Key

1. Go to https://platform.openai.com/api-keys
2. Create new API key
3. Copy and save securely

#### Groq API Key

1. Go to https://console.groq.com
2. Create API key
3. Copy and save securely

#### Pinecone API Key

1. Go to https://www.pinecone.io
2. Create account and project
3. Get API key from project settings
4. Create index with dimension 1536 (for OpenAI embeddings)

#### Cloudinary

1. Go to https://cloudinary.com
2. Sign up for free account
3. Get API credentials from dashboard

### Running Development Server

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

The Python backend will be available at `http://localhost:8000`

### API Documentation

- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc

## 4. External Services Setup

### Google OAuth Setup

1. Go to https://console.cloud.google.com
2. Create new project
3. Enable Google+ API
4. Create OAuth 2.0 credentials (Web application)
5. Add authorized redirect URIs:
   - `http://localhost:3001/api/auth/google/callback` (development)
   - `https://your-domain.com/api/auth/google/callback` (production)
6. Copy Client ID and Client Secret to `.env`

### Redis Setup (Optional)

#### Local Redis

```bash
# macOS with Homebrew
brew install redis
brew services start redis

# Connection string
redis://localhost:6379
```

#### Redis Cloud

1. Go to https://redis.com/try-free/
2. Create free database
3. Get connection string
4. Add to `REDIS_URL` in `.env`

## 5. Running All Services

### Terminal 1: Frontend

```bash
cd client
npm run dev
```

### Terminal 2: Backend

```bash
cd server
npm run dev
```

### Terminal 3: Python Backend

```bash
cd python-backend
source venv/bin/activate  # or venv\Scripts\activate on Windows
uvicorn main:app --reload
```

### Verify All Services

```bash
# Frontend
curl http://localhost:5173

# Backend
curl http://localhost:3001/api/health

# Python Backend
curl http://localhost:8000
```

## 6. Database Seeding (Optional)

To populate the database with sample data:

```bash
cd server
# Create a seed script in prisma/seed.js
npm run db:seed
```

## 7. Docker Setup (Optional)

### Build Docker Images

```bash
# Backend
cd server
docker build -t edulume-server .
docker run -p 3001:3001 --env-file .env edulume-server

# Python Backend
cd python-backend
docker build -t edulume-python .
docker run -p 8000:8080 --env-file .env edulume-python
```

### Docker Compose

Create `docker-compose.yml` in root directory:

```yaml
version: "3.8"

services:
  mongodb:
    image: mongo:latest
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_DATABASE: edulume

  redis:
    image: redis:latest
    ports:
      - "6379:6379"

  backend:
    build: ./server
    ports:
      - "3001:3001"
    environment:
      DATABASE_URL: mongodb://mongodb:27017/edulume
      REDIS_URL: redis://redis:6379
    depends_on:
      - mongodb
      - redis

  python-backend:
    build: ./python-backend
    ports:
      - "8000:8080"
    environment:
      ALLOWED_ORIGINS: http://localhost:5173,http://localhost:3001

  frontend:
    build: ./client
    ports:
      - "5173:5173"
    environment:
      VITE_API_URL: http://localhost:3001/api
      VITE_SOCKET_URL: http://localhost:3001
      VITE_PYTHON_API_URL: http://localhost:8000
```

Run with:

```bash
docker-compose up
```

## 8. Troubleshooting

### MongoDB Connection Issues

- Verify connection string is correct
- Check MongoDB is running (local) or accessible (cloud)
- Ensure IP whitelist includes your machine (Atlas)

### JWT Token Errors

- Ensure `JWT_SECRET` is set in `.env`
- Check token hasn't expired (7 days)
- Verify token format: `Bearer <token>`

### CORS Errors

- Add your frontend URL to `CLIENT_ORIGIN` in backend `.env`
- Verify CORS middleware is configured correctly
- Check browser console for specific CORS error

### Email Not Sending

- Verify Gmail App Password is correct (not regular password)
- Enable "Less secure app access" if using regular password
- Check SMTP settings are correct
- Verify `FROM_EMAIL` matches SMTP_USER

### Pinecone Connection Issues

- Verify API key is correct
- Check index exists and has correct dimension (1536)
- Ensure environment region is correct

### Python Backend Import Errors

- Verify virtual environment is activated
- Run `pip install -r requirements.txt` again
- Check Python version is 3.11+

## 9. Development Tips

### Hot Reload

- Frontend: Automatic with Vite
- Backend: Automatic with `--watch` flag
- Python: Automatic with `--reload` flag

### Database Inspection

```bash
# Open Prisma Studio
cd server
npm run db:studio
```

### API Testing

Use Postman or Insomnia:

- Import API collection from `server/postman-collection.json`
- Set environment variables
- Test endpoints

### Logging

- Frontend: Browser DevTools Console
- Backend: Terminal output with emoji indicators
- Python: Terminal output with logging module

## 10. Production Deployment

See deployment guides:

- **Frontend**: Vercel deployment guide
- **Backend**: Fly.io deployment guide
- **Python Backend**: Fly.io deployment guide

## 📚 Additional Resources

- [Express.js Documentation](https://expressjs.com/)
- [Prisma Documentation](https://www.prisma.io/docs/)
- [React Documentation](https://react.dev/)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [Socket.io Documentation](https://socket.io/docs/)

## ❓ Getting Help

1. Check existing issues in repository
2. Review error messages carefully
3. Check `.env` file configuration
4. Verify all services are running
5. Check network connectivity
6. Review logs for specific errors

---

**Happy coding! 🚀**
