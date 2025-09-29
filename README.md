# 🚀 Project Management System - Backend API

A robust Node.js backend API for the project management system, built with Express.js, MongoDB, and TypeScript. Provides comprehensive workspace management, project tracking, and task organization with role-based access control.

## ✨ Features

### 🔐 Authentication & Security
- **Multiple Auth Methods**:
  - Local authentication (email/password)
  - Google OAuth 2.0 integration
- **Secure Session Management**: Cookie-based sessions with proper security
- **Password Encryption**: Bcrypt hashing for secure password storage
- **CORS Configuration**: Proper cross-origin resource sharing setup

### 🏢 Workspace Management API
- **Multi-workspace Support**: Create and manage multiple workspaces
- **Role-based Access Control**: Owner, Admin, and Member roles with granular permissions
- **Member Management**: Invite, remove, and manage workspace members
- **Workspace Analytics**: Track workspace performance and metrics

### 📊 Project Management API
- **Project CRUD Operations**: Create, read, update, delete projects
- **Project Analytics**: Monitor project progress and performance
- **Permission-based Access**: Control who can create, edit, and delete projects

### ✅ Task Management API
- **Task Status Tracking**: Backlog, Todo, In Progress, In Review, Done
- **Priority Levels**: Low, Medium, High priority tasks
- **Task Assignment**: Assign tasks to workspace members
- **Task Analytics**: Track task completion and performance metrics

## 🛠️ Tech Stack

### Core Technologies
- **Runtime**: Node.js
- **Framework**: Express.js
- **Language**: TypeScript
- **Database**: MongoDB with Mongoose ODM

### Authentication & Security
- **Authentication**: Passport.js (Local & Google OAuth)
- **Session Management**: cookie-session
- **Password Hashing**: bcrypt
- **CORS**: cors middleware

### Validation & Utilities
- **Schema Validation**: Zod
- **Environment Variables**: dotenv
- **UUID Generation**: uuid
- **Development**: ts-node-dev for hot reloading

## 📁 Project Structure

```
backend/
├── src/
│   ├── config/                 # Configuration files
│   │   ├── app.config.ts      # Application configuration
│   │   ├── database.config.ts  # Database connection
│   │   ├── http.config.ts     # HTTP status codes
│   │   └── passport.config.ts  # Passport strategies
│   ├── controllers/           # Route controllers
│   │   ├── auth.controller.ts
│   │   ├── member.controller.ts
│   │   ├── project.controller.ts
│   │   ├── task.controller.ts
│   │   ├── user.controller.ts
│   │   └── workspace.controller.ts
│   ├── enums/                 # TypeScript enums
│   │   ├── account-provider.enum.ts
│   │   ├── error-code.enum.ts
│   │   ├── role.enum.ts
│   │   └── task.enum.ts
│   ├── middlewares/           # Express middlewares
│   │   ├── asyncHandler.middleware.ts
│   │   ├── errorHandler.middleware.ts
│   │   └── isAuthenticated.middleware.ts
│   ├── models/               # Mongoose models
│   │   ├── account.model.ts
│   │   ├── member.model.ts
│   │   ├── project.model.ts
│   │   ├── roles-permission.model.ts
│   │   ├── task.model.ts
│   │   ├── user.model.ts
│   │   └── workspace.model.ts
│   ├── routes/               # API routes
│   │   ├── auth.route.ts
│   │   ├── member.route.ts
│   │   ├── project.route.ts
│   │   ├── task.route.ts
│   │   ├── user.route.ts
│   │   └── workspace.route.ts
│   ├── seeders/              # Database seeders
│   │   └── role.seeder.ts
│   ├── services/             # Business logic
│   │   ├── auth.service.ts
│   │   ├── member.service.ts
│   │   ├── project.service.ts
│   │   ├── task.service.ts
│   │   ├── user.service.ts
│   │   └── workspace.service.ts
│   ├── utils/                # Utility functions
│   │   ├── appError.ts
│   │   ├── bcrypt.ts
│   │   ├── get-env.ts
│   │   ├── role-permission.ts
│   │   ├── roleGuard.ts
│   │   └── uuid.ts
│   ├── validation/           # Zod schemas
│   │   ├── auth.validation.ts
│   │   ├── project.validation.ts
│   │   ├── task.validation.ts
│   │   └── workspace.validation.ts
│   └── index.ts              # Application entry point
├── package.json
└── tsconfig.json
```

## 🚀 Getting Started

### Prerequisites
- Node.js (v16 or higher)
- MongoDB database
- npm or yarn package manager

### Environment Variables

Create a `.env` file in the backend directory:

```env
# Database
MONGODB_URI=mongodb://localhost:27017/project-management

# Authentication
SESSION_SECRET=your-session-secret-key-here
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret

# Frontend URL
FRONTEND_ORIGIN=http://localhost:5173
FRONTEND_GOOGLE_CALLBACK_URL=http://localhost:5173/auth/callback

# Server Configuration
PORT=5000
NODE_ENV=development
```

### Installation & Setup

1. **Install dependencies**
```bash
npm install
```

2. **Setup database**
```bash
npm run seed  # Seed initial roles
```

3. **Start development server**
```bash
npm run dev
```

4. **Build for production**
```bash
npm run build
npm start
```

The API server will be available at http://localhost:5000

## 📊 API Endpoints

### Authentication Routes
```
POST   /api/auth/register              # User registration
POST   /api/auth/login                 # User login
POST   /api/auth/logout                # User logout
GET    /api/auth/google                # Google OAuth login
GET    /api/auth/google/callback       # Google OAuth callback
```

### User Routes
```
GET    /api/users/profile              # Get current user profile
PUT    /api/users/profile              # Update user profile
```

### Workspace Routes
```
GET    /api/workspaces                 # Get user workspaces
POST   /api/workspaces                 # Create workspace
GET    /api/workspaces/:id             # Get workspace details
PUT    /api/workspaces/:id             # Update workspace
DELETE /api/workspaces/:id             # Delete workspace
GET    /api/workspaces/:id/analytics   # Get workspace analytics
GET    /api/workspaces/:id/members     # Get workspace members
POST   /api/workspaces/:id/members     # Add workspace member
PUT    /api/workspaces/:id/members/:memberId/role  # Change member role
DELETE /api/workspaces/:id/members/:memberId       # Remove member
```

### Project Routes
```
GET    /api/workspaces/:workspaceId/projects                    # Get workspace projects
POST   /api/workspaces/:workspaceId/projects                    # Create project
GET    /api/workspaces/:workspaceId/projects/:id               # Get project details
PUT    /api/workspaces/:workspaceId/projects/:id               # Update project
DELETE /api/workspaces/:workspaceId/projects/:id               # Delete project
GET    /api/workspaces/:workspaceId/projects/:id/analytics     # Get project analytics
```

### Task Routes
```
GET    /api/workspaces/:workspaceId/projects/:projectId/tasks           # Get project tasks
POST   /api/workspaces/:workspaceId/projects/:projectId/tasks           # Create task
GET    /api/workspaces/:workspaceId/projects/:projectId/tasks/:id       # Get task details
PUT    /api/workspaces/:workspaceId/projects/:projectId/tasks/:id       # Update task
DELETE /api/workspaces/:workspaceId/projects/:projectId/tasks/:id       # Delete task
```

## 🔒 Permissions System

### Roles
- **OWNER**: Full access to workspace
- **ADMIN**: Management permissions (cannot delete workspace)
- **MEMBER**: Basic access permissions

### Permissions Matrix
```typescript
const Permissions = {
  // Workspace permissions
  CREATE_WORKSPACE: "CREATE_WORKSPACE",
  DELETE_WORKSPACE: "DELETE_WORKSPACE",
  EDIT_WORKSPACE: "EDIT_WORKSPACE",
  MANAGE_WORKSPACE_SETTINGS: "MANAGE_WORKSPACE_SETTINGS",

  // Member permissions
  ADD_MEMBER: "ADD_MEMBER",
  CHANGE_MEMBER_ROLE: "CHANGE_MEMBER_ROLE",
  REMOVE_MEMBER: "REMOVE_MEMBER",

  // Project permissions
  CREATE_PROJECT: "CREATE_PROJECT",
  EDIT_PROJECT: "EDIT_PROJECT",
  DELETE_PROJECT: "DELETE_PROJECT",

  // Task permissions
  CREATE_TASK: "CREATE_TASK",
  EDIT_TASK: "EDIT_TASK",
  DELETE_TASK: "DELETE_TASK",
  ASSIGN_TASK: "ASSIGN_TASK",
};
```

## 🏗️ Architecture

### Design Patterns
- **MVC Architecture**: Clear separation of Models, Views (routes), and Controllers
- **Service Layer**: Business logic abstracted into service classes
- **Middleware Pattern**: Authentication, error handling, and validation middlewares
- **Repository Pattern**: Data access through Mongoose models

### Key Features
- **Type Safety**: Full TypeScript implementation
- **Validation**: Zod schemas for request validation
- **Error Handling**: Centralized error handling with custom error classes
- **Security**: Secure authentication with proper session management
- **Database**: MongoDB with Mongoose ODM for data modeling

### Database Models
- **User**: User account information
- **Account**: OAuth account linkage
- **Workspace**: Project workspace container
- **Member**: Workspace membership with roles
- **Project**: Project information within workspaces
- **Task**: Task information within projects
- **RolesPermission**: Role-based permission mapping

## 🧪 Testing

```bash
# Run tests (if implemented)
npm test

# Run tests in watch mode
npm run test:watch

# Run test coverage
npm run test:coverage
```

## 🚀 Deployment

### Environment Setup
1. Set production environment variables
2. Configure MongoDB connection
3. Set up Google OAuth credentials
4. Configure CORS for production domain

### Build & Deploy
```bash
npm run build
npm start
```

## 🔧 Scripts

- `npm run dev` - Start development server with hot reload
- `npm run build` - Build TypeScript to JavaScript
- `npm start` - Start production server
- `npm run seed` - Seed database with initial roles

## 🐛 Error Handling

The API uses centralized error handling with custom error classes:

- **AppError**: Custom application errors
- **ValidationError**: Zod validation errors
- **AuthenticationError**: Authentication failures
- **AuthorizationError**: Permission denied errors

## 📝 API Response Format

### Success Response
```json
{
  "data": {},
  "message": "Success message"
}
```

### Error Response
```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Error description"
  }
}
```

## 🤝 Contributing

1. Follow TypeScript best practices
2. Use Zod for validation schemas
3. Implement proper error handling
4. Write comprehensive tests
5. Follow the existing project structure

## 📞 Support

For backend-specific issues, please check:
1. Database connection
2. Environment variables
3. Authentication configuration
4. API endpoint documentation

---

Built with ❤️ using Node.js, Express, and TypeScript