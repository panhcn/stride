# App Directory

This directory contains the core application code for the Rails backend.

## Directory Structure

- `controllers/` - Controllers that handle HTTP requests
  - `concerns/` - Shared controller functionality
- `models/` - ActiveRecord models that interact with the database
  - `concerns/` - Shared model functionality
- `views/` - View templates (if applicable)
- `services/` - Service objects for complex business logic
- `jobs/` - Background job classes
- `mailers/` - Email sending classes
- `helpers/` - View helper methods

## Development Guidelines

### MVC Architecture

This application follows the Model-View-Controller (MVC) pattern:
- Models handle data and business logic
- Views handle presentation (API responses in JSON format)
- Controllers handle HTTP requests and responses

### Code Organization

- Keep controllers thin - move complex logic to service objects
- Use concerns for shared functionality
- Follow the single responsibility principle
- Use meaningful naming conventions

### Type Safety

As specified in the server README, type safety is enforced:
- New code must be `# typed: strict` minimum
- Full type signatures required
- No `T.untyped` in public APIs
- Test coverage with types
