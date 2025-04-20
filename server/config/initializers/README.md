# Initializers Directory

This directory contains initialization code that runs when the Rails application starts.

## Purpose

Initializers are used to:
- Configure Rails components
- Set up third-party libraries
- Define constants
- Configure middleware
- Set application defaults
- Extend Rails functionality

## Common Initializers

- `cors.rb` - Configure Cross-Origin Resource Sharing
- `filter_parameter_logging.rb` - Configure parameter filtering in logs
- `inflections.rb` - Configure custom inflections
- `mime_types.rb` - Register custom MIME types
- `permissions_policy.rb` - Configure permissions policy headers

## Execution Order

Initializers are executed in alphabetical order. If the order is important, you can prefix the filenames with numbers:
- `01_critical_first.rb`
- `02_depends_on_first.rb`
- `03_less_important.rb`

## Example Initializers

### CORS Configuration

```ruby
# config/initializers/cors.rb
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins 'example.com', 'localhost:3000'
    
    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head],
      credentials: true
  end
end
```

### Parameter Filtering

```ruby
# config/initializers/filter_parameter_logging.rb
Rails.application.config.filter_parameters += [
  :passw, :secret, :token, :_key, :crypt, :salt, :certificate, :otp, :ssn
]
```

### Custom Inflections

```ruby
# config/initializers/inflections.rb
ActiveSupport::Inflector.inflections(:en) do |inflect|
  inflect.acronym 'API'
  inflect.irregular 'person', 'people'
  inflect.uncountable %w( fish sheep )
end
```

### Third-Party Library Configuration

```ruby
# config/initializers/aws.rb
Aws.config.update({
  region: ENV['AWS_REGION'],
  credentials: Aws::Credentials.new(
    ENV['AWS_ACCESS_KEY_ID'],
    ENV['AWS_SECRET_ACCESS_KEY']
  )
})
```

## Best Practices

1. Keep initializers focused and small
2. Use environment variables for configuration
3. Document complex initializers
4. Be mindful of initialization order
5. Handle errors gracefully
6. Avoid expensive operations in initializers
7. Test initializers thoroughly
8. Use descriptive filenames
