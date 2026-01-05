# Cloud Memory

A self-hosted photo gallery application built with Go. Create galleries, upload images, and organize your memories in the cloud.

## Features

- **Gallery Management** — Create, edit, and delete photo galleries
- **Image Upload** — Upload images via file upload or URL
- **User Authentication** — Sign up, sign in, password reset via email
- **Dropbox Integration** — Connect your Dropbox account to import images
- **CSRF Protection** — Secure form submissions with gorilla/csrf
- **Database Migrations** — Automatic schema management with Goose
- **Docker Ready** — Production and development Docker Compose configs

## Tech Stack

| Component | Technology |
|-----------|------------|
| Language | Go 1.25 |
| Router | Chi |
| Database | PostgreSQL |
| Migrations | Goose |
| Templates | Go html/template |
| Styling | Tailwind CSS |
| Email | go-mail (SMTP) |
| OAuth | golang.org/x/oauth2 |
| Reverse Proxy | Caddy |

## Getting Started

### Prerequisites

- Go 1.25+
- PostgreSQL 14+
- Docker & Docker Compose (optional)

### Configuration

Copy the environment template and fill in your values:

```bash
cp .env.template .env
```

**Required environment variables:**
```bash
# Copy and edit the .env.template into your .env
```
Generate a CSRF key:

```bash
openssl rand -hex 32
```

### Running Locally

```bash
# Start PostgreSQL (if using Docker)
docker compose up -d db

# Run the application
go run cmd/server.go
```

### Running with Docker

**Development:**

```bash
docker compose up
```

**Production:**

```bash
docker compose -f docker-compose.yml -f docker-compose.production.yml up -d
```

## Project Structure

```
cloud-memory/
├── cmd/                    # Application entrypoint
├── controllers/            # HTTP handlers
├── models/                 # Data models and database logic
├── views/                  # Template rendering
├── templates/              # HTML templates (gohtml)
├── migrations/             # Database migrations (SQL)
├── context/                # Request context helpers
├── errors/                 # Custom error types
├── rand/                   # Random string generation
├── assets/                 # Static files (CSS, JS, images)
├── tailwind/               # Tailwind CSS config
├── Dockerfile
├── docker-compose.yml
├── docker-compose.production.yml
└── Caddyfile               # Reverse proxy config
```

## API Routes

| Method | Path | Description | Auth |
|--------|------|-------------|------|
| GET | `/` | Home page | No |
| GET | `/contact` | Contact page | No |
| GET | `/faq` | FAQ page | No |
| GET | `/signup` | Registration form | No |
| POST | `/users` | Create user | No |
| GET | `/signin` | Login form | No |
| POST | `/signin` | Process login | No |
| POST | `/signout` | Logout | Yes |
| GET | `/forgot-pw` | Password reset form | No |
| POST | `/forgot-pw` | Send reset email | No |
| GET | `/reset-pw` | Reset password form | No |
| POST | `/reset-pw` | Process reset | No |
| GET | `/users/me` | Current user profile | Yes |
| GET | `/galleries` | List user galleries | Yes |
| GET | `/galleries/new` | New gallery form | Yes |
| POST | `/galleries` | Create gallery | Yes |
| GET | `/galleries/{id}` | View gallery | No |
| GET | `/galleries/{id}/edit` | Edit gallery form | Yes |
| POST | `/galleries/{id}` | Update gallery | Yes |
| POST | `/galleries/{id}/delete` | Delete gallery | Yes |
| POST | `/galleries/{id}/images` | Upload images | Yes |
| POST | `/galleries/{id}/images/url` | Add images via URL | Yes |
| GET | `/galleries/{id}/images/{filename}` | Serve image | No |
| POST | `/galleries/{id}/images/{filename}/delete` | Delete image | Yes |
| GET | `/oauth/{provider}/connect` | Start OAuth flow | Yes |
| GET | `/oauth/{provider}/callback` | OAuth callback | Yes |

## Development

### Database Migrations

Migrations run automatically on startup. To create a new migration:

```bash
goose -dir migrations create  sql
```

### Building

```bash
go build -o cloud-memory ./cmd/server.go
```

### Testing

```bash
go test ./...
```

## Author

[Rahul4469](https://github.com/Rahul4469)
