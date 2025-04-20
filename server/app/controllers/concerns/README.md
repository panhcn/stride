# Controller Concerns Directory

This directory contains modules that can be included in controllers to share functionality.

## Purpose

Controller concerns are used to:
- Extract and share common functionality between controllers
- Keep controllers DRY (Don't Repeat Yourself)
- Organize cross-cutting concerns like authentication, authorization, error handling, etc.

## Best Practices

### When to Use Concerns

Use concerns when:
- Multiple controllers need the same functionality
- A controller is getting too large and complex
- Functionality is distinct and can be isolated

### Structure of a Concern

```ruby
# typed: strict
module Authenticable
  extend ActiveSupport::Concern
  extend T::Sig
  
  included do
    before_action :authenticate_user
  end
  
  sig { returns(T.nilable(User)) }
  def current_user
    @current_user ||= User.find_by(id: session[:user_id])
  end
  
  private
  
  sig { void }
  def authenticate_user
    unless current_user
      render json: { error: 'Unauthorized' }, status: :unauthorized
    end
  end
end
```

### Implementation Example

```ruby
# In a controller
class ApiController < ApplicationController
  include Authenticable
  
  # This controller now has authentication functionality
end
```

## Common Concerns

- Authentication
- Authorization
- Error handling
- Pagination
- Filtering
- Sorting
- Logging
- Caching

## Type Safety

As with all code in the application:
- Use `# typed: strict` or higher
- Include full type signatures
- Test thoroughly
