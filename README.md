# Todo App - FastAPI Backend

A modern, secure todo application built with FastAPI, featuring user authentication, CRUD operations, and a clean modular architecture.

## Features

- 🔐 **User Authentication** - JWT-based secure login/registration
- ✅ **Todo Management** - Create, read, update, delete todos
- 👤 **User-specific Todos** - Each user only sees their own todos
- 🗄️ **SQLite Database** - Lightweight database with SQLAlchemy ORM
- 🏗️ **Modular Architecture** - Clean separation of concerns
- 📝 **Auto-generated API Docs** - Interactive Swagger/OpenAPI documentation
- 🚀 **Production Ready** - Deployed on Railway

## Tech Stack

- **Framework**: FastAPI
- **Database**: SQLite with SQLAlchemy ORM
- **Authentication**: JWT tokens with bcrypt password hashing
- **Server**: Uvicorn ASGI server
- **Deployment**: Railway

## Project Structure

```
to-do-app/
├── main.py          # FastAPI application and API routes
├── auth.py          # Authentication logic and JWT handling
├── database.py      # Database configuration and connection
├── models.py        # SQLAlchemy database models
├── schemas.py       # Pydantic schemas for request/response validation
├── requirements.txt # Python dependencies
├── static/          # Static files (HTML, CSS, JS)
│   └── index.html   # Frontend interface
└── todos.db         # SQLite database file (auto-generated)
```

## API Endpoints

### Authentication
- `POST /api/register` - Register a new user
- `POST /api/login` - Login user and get JWT token
- `GET /api/me` - Get current user information

### Todos
- `GET /api/todos` - Get all todos for authenticated user
- `POST /api/todos` - Create a new todo
- `PUT /api/todos/{todo_id}` - Update a specific todo
- `DELETE /api/todos/{todo_id}` - Delete a specific todo

### Frontend
- `GET /` - Serve the main HTML interface

## Quick Start

### Prerequisites
- Python 3.8+
- pip

### Local Development

1. **Clone the repository**
   ```bash
   git clone https://github.com/NeuralNoble/to-do-app
   cd to-do-app
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv fastapi
   source fastapi/bin/activate  # On Windows: fastapi\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application**
   ```bash
   uvicorn main:app --reload --port 8001
   ```

5. **Access the application**
   - Frontend: http://localhost:8001
   - API Documentation: http://localhost:8001/docs
   - Alternative docs: http://localhost:8001/redoc

## Database Schema

### Users Table
- `id` - Primary key
- `username` - Unique username
- `email` - Unique email address
- `hashed_password` - Bcrypt hashed password
- `created_at` - Account creation timestamp

### Todos Table
- `id` - Primary key
- `title` - Todo title
- `description` - Optional todo description
- `completed` - Boolean completion status
- `created_at` - Todo creation timestamp
- `user_id` - Foreign key to users table

## Authentication Flow

1. User registers with username, email, and password
2. Password is hashed using bcrypt
3. User logs in with username/password
4. Server returns JWT access token
5. Client includes token in Authorization header for protected routes
6. Server validates token and returns user-specific data

## Security Features

- **Password Hashing**: Bcrypt with salt for secure password storage
- **JWT Tokens**: Stateless authentication with 30-minute expiration
- **User Isolation**: Users can only access their own todos
- **Input Validation**: Pydantic schemas validate all request data
- **CORS Enabled**: Cross-origin requests supported

## Deployment

The application is deployed on Railway and accessible at your deployment URL.

### Environment Variables (if needed)
- `SECRET_KEY` - JWT signing secret (default provided for development)
- `DATABASE_URL` - Database connection string (SQLite file by default)

## API Usage Examples

### Register a new user
```bash
curl -X POST "http://localhost:8001/api/register" \
  -H "Content-Type: application/json" \
  -d '{
    "username": "johndoe",
    "email": "john@example.com",
    "password": "securepassword"
  }'
```

### Login
```bash
curl -X POST "http://localhost:8001/api/login" \
  -H "Content-Type: application/json" \
  -d '{
    "username": "johndoe",
    "password": "securepassword"
  }'
```

### Create a todo (requires authentication)
```bash
curl -X POST "http://localhost:8001/api/todos" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -d '{
    "title": "Learn FastAPI",
    "description": "Build a todo app with FastAPI"
  }'
```

## Development

### Code Structure
- **Modular Design**: Separated into auth, database, models, and schemas
- **Type Hints**: Full type annotation throughout the codebase
- **Error Handling**: Comprehensive HTTP exception handling
- **Documentation**: Auto-generated OpenAPI/Swagger docs


