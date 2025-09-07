# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview

EduCloud is a full-stack educational cloud platform with the following structure:
- `backend/` - API server and business logic
- `frontend/` - Web application interface  
- `database/` - Database schemas, migrations, and seed data
- `docs/` - Documentation and API specs
- `scripts/` - Build, deployment, and utility scripts

## Development Commands

### Getting Started
```bash
# Clone and setup (if not already done)
git clone <repository-url>
cd educloud

# Install dependencies for all components
./scripts/setup.sh

# Start development environment
./scripts/dev.sh
```

### Backend Development
```bash
# Navigate to backend
cd backend/

# Install dependencies
npm install
# or
pip install -r requirements.txt
# (depends on chosen backend technology)

# Start development server
npm run dev
# or  
python manage.py runserver
# or
go run main.go

# Run tests
npm test
# or
python -m pytest
# or
go test ./...

# Run single test file
npm test -- --testPathPattern=tests/auth.test.js
# or
python -m pytest tests/test_auth.py
# or
go test ./auth

# Lint code
npm run lint
# or
flake8 .
# or
golangci-lint run

# Format code
npm run format
# or
black .
# or
gofmt -w .
```

### Frontend Development
```bash
# Navigate to frontend
cd frontend/

# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Run tests
npm test

# Run single test
npm test -- Button.test.jsx

# Lint and format
npm run lint
npm run format
```

### Database Operations
```bash
# Navigate to database directory
cd database/

# Run migrations
./migrate.sh up
# or
python manage.py migrate
# or
npm run migrate

# Rollback migration
./migrate.sh down 1

# Seed development data
./seed.sh dev
# or
python manage.py loaddata fixtures/dev_data.json

# Backup database
./backup.sh production backup_$(date +%Y%m%d)
```

### Full Stack Development
```bash
# Start entire development environment
docker-compose up -d

# View logs for all services
docker-compose logs -f

# Restart specific service
docker-compose restart backend

# Stop all services
docker-compose down
```

## Architecture Overview

### Backend Architecture
The backend follows a layered architecture pattern:
- **Controllers** - Handle HTTP requests and responses
- **Services** - Business logic and core functionality  
- **Repositories** - Data access layer and database operations
- **Models** - Data structures and entity definitions
- **Middleware** - Authentication, logging, error handling
- **Utils** - Shared utilities and helper functions

### API Design
- RESTful API design with consistent naming conventions
- JWT-based authentication for user sessions
- Role-based access control (RBAC) for authorization
- API versioning through URL prefixing (`/api/v1/`)
- OpenAPI/Swagger documentation for all endpoints

### Frontend Architecture
- Component-based architecture using React/Vue.js
- State management with Redux/Vuex for global state
- Routing for single-page application navigation
- Responsive design with mobile-first approach
- Modular CSS/SCSS organization

### Database Schema
- User management (students, teachers, administrators)
- Course catalog and enrollment system
- Assignment and grading workflow
- Discussion forums and messaging
- File storage and content management
- Analytics and reporting data

## Key Integration Points

### Authentication Flow
1. User registration/login through frontend
2. Backend validates credentials and issues JWT
3. Frontend stores token and includes in API requests
4. Backend middleware validates token on protected routes

### File Upload System
1. Frontend uploads files to backend endpoint
2. Backend validates file type and size limits
3. Files stored in cloud storage (AWS S3/Azure Blob)
4. Database stores file metadata and access permissions

### Real-time Features
- WebSocket connections for live chat/notifications
- Server-sent events for real-time updates
- Message queuing for background job processing

### External Integrations
- Email service for notifications (SendGrid/Mailgun)
- Payment processing for course purchases (Stripe)
- Video conferencing integration (Zoom/WebRTC)
- Learning management system (LMS) compatibility

## Environment Configuration

### Development
- Hot reloading enabled for rapid development
- Debug logging and error reporting
- Mock external services for testing
- Seed data for consistent development state

### Testing  
- Unit tests for individual components
- Integration tests for API endpoints
- End-to-end tests for user workflows
- Performance testing for scalability

### Production
- Containerized deployment with Docker
- Load balancing and auto-scaling
- SSL/TLS encryption for all traffic
- Monitoring and alerting systems

## Security Considerations

### Data Protection
- Input validation and sanitization
- SQL injection prevention
- Cross-site scripting (XSS) protection
- Cross-site request forgery (CSRF) tokens

### Access Control
- Multi-factor authentication (MFA) support
- Session management and timeout policies
- API rate limiting and throttling
- Audit logging for sensitive operations

## Performance Optimization

### Database
- Query optimization and indexing
- Connection pooling for efficiency
- Caching frequently accessed data
- Database replication for read scaling

### API
- Response compression (gzip)
- CDN for static asset delivery
- API response caching strategies
- Pagination for large data sets

### Frontend
- Code splitting and lazy loading
- Image optimization and compression  
- Browser caching configurations
- Performance monitoring and metrics

This architecture supports a scalable, maintainable educational platform that can grow with user demand while maintaining security and performance standards.
