# Lib Directory

This directory contains library code and modules that don't fit into the standard Rails MVC structure.

## Purpose

The lib directory is used for:
- Custom modules and classes
- Extensions to Ruby or Rails
- Utility functions
- External service integrations
- Tasks and rake tasks

## Directory Structure

- `tasks/` - Custom rake tasks
- Other directories for organizing library code

## When to Use Lib

Use the lib directory for code that:
- Doesn't belong in models, controllers, or views
- Is reusable across different parts of the application
- Extends or modifies Ruby or Rails functionality
- Integrates with external services
- Implements utility functions

## Example Library Code

### Utility Module

```ruby
# typed: strict
module Utils
  module StringUtils
    extend T::Sig
    
    sig { params(str: String).returns(String) }
    def self.sanitize(str)
      str.strip.gsub(/[^0-9A-Za-z\s]/, '')
    end
    
    sig { params(str: String).returns(String) }
    def self.titleize(str)
      str.split(' ').map(&:capitalize).join(' ')
    end
  end
end
```

### External Service Integration

```ruby
# typed: strict
module Services
  class PaymentGateway
    extend T::Sig
    
    sig { params(api_key: String).void }
    def initialize(api_key)
      @api_key = api_key
    end
    
    sig do
      params(
        amount: Integer,
        currency: String,
        card_token: String
      ).returns(T::Hash[Symbol, T.untyped])
    end
    def charge(amount:, currency:, card_token:)
      # Implementation
    end
  end
end
```

## Custom Rake Tasks

Custom rake tasks are stored in the `tasks/` directory and are loaded automatically by Rails.

### Example Rake Task

```ruby
# lib/tasks/data.rake
namespace :data do
  desc "Import data from CSV file"
  task import: :environment do
    puts "Importing data..."
    # Implementation
    puts "Import complete!"
  end
end
```

### Running Rake Tasks

```bash
# Run a custom rake task
bin/rails data:import
```

## Best Practices

1. Keep library code focused and well-organized
2. Document library code thoroughly
3. Write tests for library code
4. Follow the same coding standards as the rest of the application
5. Use namespaces to organize code
6. Consider extracting widely reusable code into gems
