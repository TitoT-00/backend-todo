# Backend TODO API

A REST API for task management built with Express.js and Prisma with SQLite.

## Features

- **CRUD Operations**: Create, Read, Update, and Delete tasks
- **Task Properties**: Each task includes id, title, color, completed status, and timestamps
- **SQLite Database**: Uses Prisma ORM for database operations
- **Input Validation**: Comprehensive validation for all endpoints
- **Error Handling**: Proper error responses and logging

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/tasks` | Retrieve all tasks |
| POST | `/tasks` | Create a new task |
| PUT | `/tasks/:id` | Update an existing task |
| DELETE | `/tasks/:id` | Delete a task |

## Task Schema

```json
{
  "id": 1,
  "title": "Complete project",
  "color": "#FF5733",
  "completed": false,
  "createdAt": "2024-01-01T00:00:00.000Z",
  "updatedAt": "2024-01-01T00:00:00.000Z"
}
```

## Quick Setup Guide

### Prerequisites
- Node.js (v14 or higher)
- npm or yarn

### Step-by-Step Installation

1. **Clone/Navigate to the project directory:**
   ```bash
   cd backend-todo
   ```

2. **Install all dependencies:**
   ```bash
   npm install
   ```

3. **Initialize Prisma database:**
   ```bash
   # Generate Prisma client
   npx prisma generate
   
   # Create SQLite database and tables
   npx prisma db push
   ```
   
   **What happens:** 
   - Creates `dev.db` SQLite file in project root
   - Generates `tasks` table with all required fields
   - No database server installation needed

4. **Start the development server:**
   ```bash
   npm run dev
   ```
   
   **Server runs on:** `http://localhost:3000`

### Verify Installation

Test the API is working:
```bash
# Health check
curl http://localhost:3000

# Get all tasks (should return empty array initially)
curl http://localhost:3000/tasks
```

### Environment Configuration
The `.env` file is pre-configured for SQLite:
```
PORT=3001
NODE_ENV=development
```

## API Usage Examples

### Create a Task
```bash
curl -X POST http://localhost:3000/tasks \
  -H "Content-Type: application/json" \
  -d '{"title": "Learn Express.js", "color": "#3498DB"}'
```

### Get All Tasks
```bash
curl http://localhost:3000/tasks
```

### Update a Task
```bash
curl -X PUT http://localhost:3000/tasks/1 \
  -H "Content-Type: application/json" \
  -d '{"completed": true}'
```

### Delete a Task
```bash
curl -X DELETE http://localhost:3000/tasks/1
```

## Database Management

- **View database**: `npm run db:studio` (opens Prisma Studio)
- **Run migrations**: `npm run db:migrate`
- **Reset database**: `npm run db:push --force-reset`

## Error Handling

The API returns appropriate HTTP status codes:
- `200`: Success
- `201`: Created
- `400`: Bad Request (validation errors)
- `404`: Not Found
- `500`: Internal Server Error
