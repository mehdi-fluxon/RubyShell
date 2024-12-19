# Full-Stack Web Application Template

A modern full-stack web application combining Ruby on Rails backend with React frontend, containerized with Docker.

## Technology Stack

### Backend (Rails 8.0.1)

- Ruby on Rails 8.0.1
- PostgreSQL database
- Propshaft asset pipeline
- Hotwire (Turbo and Stimulus)
- Solid gems for:
  - Caching
  - Job queues
  - Action Cable
- Kamal for deployment
- Thruster for HTTP optimization

### Debugging

User VSCODE's pre-configured Ruby debugger and put breakpoints in the code.

### Database (PostgreSQL)

- PostgreSQL for production and development
- Configured for:
  - Development environment via Docker Compose
  - Test environment for CI/CD
  - Production with environment variable configuration
- Automatic database creation and migration in development
- Connection pooling support
- SSL mode configuration for production

### Frontend (React)

- Create React App setup
- Prettier for code formatting
- ESLint configuration
- Web Vitals monitoring
- Development and production environment configurations

### DevOps & Tooling

- Docker containerization
- GitHub Actions CI/CD pipeline:
  - Security scanning (Brakeman)
  - JavaScript dependency auditing
  - RuboCop linting
  - Automated testing
  - PostgreSQL service container for tests

### Development Environment

- VSCode configuration for:
  - Ruby debugging
  - Code formatting
  - Language-specific settings
- Docker Compose setup
- Development database configuration

### Testing

- RSpec setup for Ruby testing
- System tests using Capybara and Selenium
- CI integration for automated testing

### Security Features

- Content Security Policy configuration
- Parameter filtering for sensitive data
- SSL enforcement in production
- Database credential management through environment variables

## Getting Started

### Prerequisites

- Docker and Docker Compose
- Ruby 3.3.6
- Node.js (for React development)
- PostgreSQL (if running locally without Docker)

### Development Setup

1. Clone the repository
2. Start the development environment:

```bash
# Stop all containers and remove volumes
docker-compose down -v

# Start the database first and wait a few seconds
docker-compose up db -d
sleep 10

# Now create the database
docker-compose run web rails db:create db:migrate

# Finally start everything
docker-compose up
```

#### Development (Docker)

The database is automatically configured when using Docker Compose:

```yaml
# config/database.yml (development)
development:
  url: <%= ENV.fetch("DATABASE_URL", "postgres://postgres:postgres@db:5432/app_development") %>
```

#### Local Development (without Docker)

To configure the database locally:

1. Make sure PostgreSQL is installed and running
2. Update database.yml or set DATABASE_URL environment variable
3. Run setup:

```bash
bin/rails db:create db:migrate
```

### Database Access

Connect to the development database:

```bash
# With Docker:
docker-compose exec db psql -U postgres

# Local PostgreSQL:
psql -U postgres -d app_development
```

### Production Database

For production, set the following environment variables:

- `DATABASE_URL`: Full PostgreSQL connection URL
- Or individual settings:
  - `DB_HOST`
  - `DB_PORT`
  - `DB_NAME`
  - `DB_USER`
  - `DB_PASSWORD`

## Deployment

This application is configured for deployment using Kamal and can be containerized using the provided Dockerfile.

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request
