# Shodh AI Coding Contest Platform

A comprehensive full-stack coding contest platform featuring real-time code judging and live leaderboards.

## 🏗️ Architecture Overview

This project consists of three main components:

- **Backend**: Spring Boot REST API with Docker-based code execution
- **Frontend**: React/Next.js with real-time polling
- **Judge**: Dockerized execution environment for secure code validation

## 🚀 Quick Start

### Prerequisites
- Docker and Docker Compose
- Java 17+
- Node.js 18+

### Setup Instructions

1. **Clone and Setup**
   ```bash
   git clone <repository-url>
   cd shodh
   ```

2. **Build Docker Judge Image**
   ```bash
   docker build -t java-judge:latest judge/
   ```

3. **Run with Docker Compose**
   ```bash
   docker-compose up --build
   ```

4. **Access the Application**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:8080
   - API Documentation: http://localhost:8080/swagger-ui.html
   - Database Console: http://localhost:8080/h2-console

### Alternative: Local Development

1. **Start Backend**
   ```bash
   cd backend
   mvn spring-boot:run
   ```

2. **Start Frontend**
   ```bash
   cd frontend
   npm run dev
   ```

## 📋 API Design

### Core Endpoints

#### Contest Management
- `GET /api/contests` - Get all active contests
- `GET /api/contests/{contestId}` - Get contest details
- `GET /api/contests/{contestId}/leaderboard` - Get live leaderboard

#### Submission Management
- `POST /api/submissions` - Submit code for evaluation
- `GET /api/submissions/{submissionId}` - Get submission status

### Request/Response Formats

#### Submit Code
```json
POST /api/submissions
{
  "contestId": 1,
  "problemId": 1,
  "username": "john_doe",
  "code": "public class Solution { ... }",
  "language": "java"
}
```

#### Submission Status
```json
GET /api/submissions/{submissionId}
{
  "submissionId": 123,
  "status": "ACCEPTED",
  "result": "All test cases passed",
  "executionTimeMs": 150,
  "memoryUsedKB": 1024
}
```

## 🎯 Design Choices & Justification

### Backend Architecture

**Service Layer Pattern**: Implemented clear separation between controllers, services, and repositories for maintainability and testability.

**Asynchronous Processing**: Used Spring's `@Async` for submission processing to prevent blocking the main thread and provide better user experience.

**Docker Integration**: Chose Docker-in-Docker approach for secure code execution with resource limits, ensuring system stability and preventing malicious code execution.

**Database Design**: Used JPA/Hibernate with proper entity relationships and constraints. Implemented both H2 for development and MySQL for production.

### Frontend Architecture

**Polling Strategy**: Implemented client-side polling for real-time updates instead of WebSockets for simplicity and reliability across different network conditions.

**Component Structure**: Used functional components with hooks for better performance and cleaner code organization.

**State Management**: Leveraged React's built-in state management with custom hooks for submission status and leaderboard updates.

**Responsive Design**: Used Tailwind CSS for modern, responsive UI that works across different screen sizes.

### Security Considerations

**Resource Limits**: Implemented strict CPU and memory limits in Docker containers to prevent resource exhaustion.

**Code Isolation**: Each submission runs in a fresh container instance with no network access to ensure security.

**Input Validation**: Comprehensive validation on both frontend and backend to prevent injection attacks.

**Process Management**: Proper cleanup of Docker containers and temporary files after each execution.

## 🔧 Development Setup

### Backend Development
```bash
cd backend
mvn spring-boot:run
```

### Frontend Development
```bash
cd frontend
npm install
npm run dev
```

### Database
The application uses H2 in-memory database for development. For production, configure MySQL or PostgreSQL in `application.yml`.

## 🧪 Testing

### Backend Tests
```bash
cd backend
mvn test
```

### Frontend Tests
```bash
cd frontend
npm test
```

## 📁 Project Structure

```
shodh/
├── backend/                 # Spring Boot application
│   ├── src/main/java/
│   │   └── com/shodh/
│   │       ├── controller/  # REST controllers
│   │       ├── service/     # Business logic
│   │       ├── repository/  # Data access
│   │       ├── model/       # JPA entities
│   │       ├── dto/         # Data transfer objects
│   │       ├── judge/       # Code execution service
│   │       └── config/      # Configuration
│   ├── Dockerfile          # Backend container
│   └── pom.xml
├── frontend/               # Next.js application
│   ├── src/
│   │   ├── app/            # Next.js pages
│   │   ├── components/     # React components
│   │   ├── hooks/          # Custom hooks
│   │   ├── lib/            # API services
│   │   └── types/          # TypeScript types
│   ├── Dockerfile          # Frontend container
│   └── package.json
├── judge/                  # Code execution environment
│   └── Dockerfile          # Judge container
└── docker-compose.yml      # Orchestration
```

## 🎮 How to Use

1. **Join a Contest**: Enter contest ID (use `1` for the sample contest) and your username
2. **Select a Problem**: Choose from the available problems in the left sidebar
3. **Write Code**: Use the code editor to write your Java solution
4. **Submit**: Click "Submit Code" to run your solution
5. **Monitor Progress**: Watch real-time submission status updates
6. **View Leaderboard**: See live rankings updated every 15 seconds

## 🚧 Future Enhancements

- WebSocket integration for real-time updates
- Multiple programming language support (Python, C++, JavaScript)
- Advanced contest management features
- User authentication and authorization
- Performance optimizations and caching
- Code editor with syntax highlighting
- Test case management interface
- Contest analytics and reporting

## 📝 License

This project is part of a technical assessment for Shodh AI.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📞 Support

For questions or issues, please contact the development team.