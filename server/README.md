# Server (Rails Application)

## Directory Structure
server/
├── app/         # Main application code and business logic
├── config/      # All configuration and initialization files
├── db/         # Database related files and migrations
├── spec/       # Test files
├── storage/    # File storage and persistence
├── tmp/        # Temporary files and cache
├── log/        # Application logs
└── vendor/     # Third-party code

## Ruby Environment

### Ruby Version
- Ruby 3.x is required for this project
- Do not use Ruby 2.x features

### Troubleshooting
If encountering multiple configuration errors during development or test runs:
1. This may indicate terminal environment issues
2. Verify Ruby version is 3.x (not 2.x)
3. Stop adding more files if this occurs
4. Alert the developer for terminal environment resolution

## Testing

### Test File Organization
```
spec/
├── models/                 # Unit tests for models
├── services/              # Unit tests for service objects
├── controllers/           # Unit tests for controllers
├── requests/             # Integration tests for API endpoints
├── system/               # Browser-based integration tests
├── factories/            # Factory Bot definitions
├── support/              # Test helpers and shared config
└── spec_helper.rb        # RSpec configuration
```

### Core Testing Requirements
1. Integration Tests (End-to-End)
   - Required for all endpoints
   - Must verify complete request/response cycle
   - Test both success and failure scenarios
   - Verify side effects (DB changes, jobs, emails)

2. Unit Tests
   - Required for every class
   - Must achieve high test coverage (>95%)
   - Test both public and protected methods
   - Cover edge cases and error scenarios

### Coverage Requirements
- Line Coverage: Minimum 95%
- Branch Coverage: Minimum 95%
- Method Coverage: Minimum 95%

### Running Tests
```bash
# Run all unit tests
bin/rspec

# Run specific test file
bin/rspec spec/models/user_spec.rb
bin/rspec spec/services/payment_processor_spec.rb

# Run specific test by line number
bin/rspec spec/models/user_spec.rb:42

# Run with documentation format
bin/rspec --format documentation

# Run tests that match specific text
bin/rspec -e "successful payment"

# Run all request specs
bin/rspec spec/requests/

# Run all system specs
bin/rspec spec/system/

# Run specific request spec
bin/rspec spec/requests/api/v1/users_spec.rb

# Run specific system spec
bin/rspec spec/system/authentication_spec.rb
```

### Test Database Setup
```bash
# Prepare test database
bin/rails db:test:prepare

# Reset test database
bin/rails db:test:reset
```

### Coverage Report
```bash
# Run tests with coverage report
COVERAGE=true bin/rspec

# Coverage report will be generated in coverage/index.html
```

### Integration Tests Structure
```ruby
# spec/requests/api/v1/users_controller_spec.rb
RSpec.describe "API::V1::Users", type: :request do
  describe "POST /api/v1/users" do
    context "with valid parameters" do
      let(:valid_params) { { user: attributes_for(:user) } }

      it "creates user with complete flow" do
        expect {
          post "/api/v1/users", params: valid_params
        }.to change(User, :count).by(1)
          .and change(AuditLog, :count).by(1)
          .and have_enqueued_job(WelcomeEmailJob)

        expect(response).to have_http_status(:created)
        expect(json_response).to include(
          "email" => valid_params[:user][:email],
          "status" => "active"
        )
      end
    end

    context "with invalid parameters" do
      let(:invalid_params) { { user: attributes_for(:user, email: nil) } }

      it "returns validation errors" do
        post "/api/v1/users", params: invalid_params
        expect(response).to have_http_status(:unprocessable_entity)
      end
    end
  end
end
```

### Unit Tests Structure
```ruby
# spec/services/payment_processor_spec.rb
RSpec.describe PaymentProcessor do
  describe "#process" do
    subject(:processor) { described_class.new(payment) }
    let(:payment) { create(:payment) }

    it "processes payment successfully" do
      expect(ExternalPaymentService).to receive(:charge).and_return(true)
      expect(processor.process).to be_success
    end

    context "when external service fails" do
      before do
        allow(ExternalPaymentService).to receive(:charge)
          .and_raise(PaymentError)
      end

      it "handles failure gracefully" do
        result = processor.process
        expect(result).to be_failure
        expect(result.error).to be_present
      end
    end
  end
end
```

### Test Categories Required
1. Data Validation
2. Business Logic
3. Error Handling
4. Edge Cases
5. Authorization
6. Authentication
7. API Contracts
8. Database Operations
9. Background Jobs
10. External Service Interactions

### Best Practices
1. Use factories for test data
2. Mock external services
3. Use shared examples for common behavior
4. Keep tests focused and isolated
5. Use meaningful test descriptions
6. Follow Arrange-Act-Assert pattern
7. Clean up test data after each run
8. Avoid test interdependence
9. Use database cleaner strategy
10. Minimize unnecessary database queries
11. Use appropriate test doubles
12. Parallelize test suite when possible

## Type Safety

### Core Principles
1. Progressive Type Enforcement
   - All new code must be type-checked
   - Existing code upgraded incrementally
   - Critical paths prioritized for strict typing
   - Runtime checks in production for critical flows

2. Strictness Levels
   - `# typed: false` - Legacy code only
   - `# typed: true` - Minimum for new code
   - `# typed: strict` - Required for models/services
   - `# typed: strong` - Required for critical paths

### Type Signatures

#### Model Type Signatures
```ruby
# typed: strict
class User < ApplicationRecord
  extend T::Sig

  sig { returns(String) }
  def full_name
    "#{first_name} #{last_name}"
  end

  sig do
    params(
      attributes: T::Hash[Symbol, T.untyped],
      options: T::Hash[Symbol, T.untyped]
    ).returns(T::Boolean)
  end
  def update_profile(attributes:, options: {})
    update(attributes.merge(options))
  end
end
```

#### Controller Type Signatures
```ruby
# typed: strict
class UsersController < ApplicationController
  extend T::Sig

  sig { void }
  def index
    @users = T.let(User.active, T::Array[User])
  end

  sig { returns(T.nilable(User)) }
  def current_user
    T.cast(@current_user, T.nilable(User))
  end
end
```

#### Service Type Signatures
```ruby
# typed: strict
class PaymentProcessor
  extend T::Sig

  sig do
    params(
      amount: Integer,
      currency: String,
      user: User
    ).returns(Result)
  end
  def process(amount:, currency:, user:)
    # Implementation
  end
end
```

### Type Definitions

#### Custom Types
```ruby
module Types
  class Result < T::Struct
    const :success, T::Boolean
    const :data, T.untyped
    const :errors, T::Array[String]
  end

  class Money < T::Struct
    const :amount, Integer
    const :currency, String
  end
end
```

#### Enums
```ruby
class Status < T::Enum
  enums do
    Active = new
    Pending = new
    Inactive = new
  end
end
```

### Testing Requirements

1. Type Checking in Tests
```ruby
# typed: strict
RSpec.describe User do
  extend T::Sig

  sig { void }
  def setup_test_data
    @user = T.let(create(:user), User)
  end
end
```

2. Coverage Requirements
   - Minimum 90% type coverage for new code
   - Type coverage checked in CI pipeline
   - No type errors in production code
   - Runtime checks for critical paths

### CI Integration

1. Type Checking Commands
```bash
# Basic type checking
srb tc

# With metrics
srb tc --metrics

# Generate type coverage report
srb tc --metrics-file=type-coverage.json
```

2. Required Checks
   - Type checking must pass
   - No untyped code in critical paths
   - Type coverage meets minimum threshold
   - Runtime checks configured correctly

### Best Practices

1. Type Declaration
   - Use `T.let` for variable declarations
   - Use `T.cast` for type assertions
   - Use `T.must` for non-nil assertions
   - Use `T.nilable` for optional values

2. Collection Types
```ruby
T::Array[User]           # Array of Users
T::Hash[Symbol, String]  # Hash with Symbol keys, String values
T::Set[Integer]         # Set of Integers
T::Enumerable[String]   # Any enumerable of Strings
```

3. Generic Types
```ruby
T.type_parameter(:T)    # Define type parameter
T.all(User, Comparable) # Type must implement all
T.any(String, Symbol)   # Union type
```

4. Proc Types
```ruby
T.proc.params(arg0: String).returns(Integer)
T.proc.bind(User).void
```

### Error Handling

1. Type Errors
```ruby
begin
  T.let(potentially_nil, String)
rescue TypeError => e
  # Handle type error
end
```

2. Runtime Checks
```ruby
T::Configuration.enable_checking_for_sigs
T::Configuration.default_checked_level = :always
```

### Migration Strategy

1. New Code
   - Must be `# typed: strict` minimum
   - Full type signatures required
   - No `T.untyped` in public APIs
   - Test coverage with types

2. Existing Code
   - Identify critical paths
   - Add types incrementally
   - Start with public APIs
   - Add runtime checks strategically

3. Priority Order
   - Models
   - Services
   - Controllers
   - Jobs
   - Helpers
   - Views

### Tooling

1. Required Tools
   - Sorbet (`srb`)
   - Tapioca (`tapioca`)
   - RBI files
   - IDE plugins

2. Development Flow
   - Generate RBI files
   - Add type signatures
   - Run type checker
   - Fix type errors
   - Commit with coverage

### Documentation

1. Type Documentation
   - Document complex types
   - Explain type decisions
   - Note runtime implications
   - Document type assumptions

2. Example
```ruby
# @param user [User] The authenticated user
# @param options [T::Hash[Symbol, T.untyped]] Processing options
# @return [Result] Processing result with type-safe data
sig do
  params(
    user: User,
    options: T::Hash[Symbol, T.untyped]
  ).returns(Result)
end
def process(user:, options: {})
```
