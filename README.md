# Stride

Stride is a full-stack web application with a React frontend and Rails backend.

## Project Structure

The project follows a client-server architecture:

- `client/` - React frontend application
- `server/` - Ruby on Rails backend application

## Getting Started

### Prerequisites

- Node.js (v16+)
- Ruby (v3.x)
- PostgreSQL

### Installation

1. Clone the repository
2. Set up the client:
   ```bash
   cd client
   npm install
   ```
3. Set up the server:
   ```bash
   cd server
   bundle install
   rails db:create db:migrate
   ```

### Running the Application

#### Development Mode

1. Start the Rails server:
   ```bash
   cd server
   rails server
   ```

2. Start the React development server:
   ```bash
   cd client
   npm run dev
   ```

## Documentation

Each directory contains its own README.md with specific documentation:

- See `client/README.md` for frontend documentation
- See `server/README.md` for backend documentation