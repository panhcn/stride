# Config Directory

This directory contains configuration files for the Rails application.

## Purpose

The config directory contains files that configure:
- Application settings
- Environment-specific settings
- Database connections
- Routes
- Initializers
- Locales
- Environments

## Directory Structure

- `application.rb` - Main application configuration
- `boot.rb` - Boots the application
- `database.yml` - Database configuration
- `environment.rb` - Environment configuration
- `routes.rb` - Application routes
- `storage.yml` - Active Storage configuration
- `environments/` - Environment-specific configurations
- `initializers/` - Initialization code
- `locales/` - Internationalization files

## Key Configuration Files

### routes.rb

Defines the routes for the application:

```ruby
Rails.application.routes.draw do
  # API routes
  namespace :api do
    namespace :v1 do
      resources :users
      resources :posts
    end
  end
  
  # Health check
  get '/health', to: 'health#index'
end
```

### database.yml

Configures database connections for different environments:

```yaml
default: &default
  adapter: postgresql
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

development:
  <<: *default
  database: app_development

test:
  <<: *default
  database: app_test

production:
  <<: *default
  database: app_production
  username: app
  password: <%= ENV['APP_DATABASE_PASSWORD'] %>
```

### application.rb

Main application configuration:

```ruby
module MyApp
  class Application < Rails::Application
    # Initialize configuration defaults
    config.load_defaults 7.0
    
    # API only
    config.api_only = true
    
    # Time zone
    config.time_zone = 'UTC'
    
    # Autoload paths
    config.autoload_paths += %W(#{config.root}/lib)
  end
end
```

## Best Practices

1. Use environment variables for sensitive information
2. Keep environment-specific configuration in the appropriate files
3. Use initializers for configuring gems and libraries
4. Keep routes organized and documented
5. Use locale files for all user-facing text
