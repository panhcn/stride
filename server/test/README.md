# Test Directory

This directory contains test files for the Rails application.

## Purpose

The test directory is used for:
- Unit tests
- Integration tests
- System tests
- Test fixtures
- Test helpers

## Directory Structure

- `controllers/` - Controller tests
- `models/` - Model tests
- `integration/` - Integration tests
- `fixtures/` - Test fixtures
- `test_helper.rb` - Test configuration

## Testing Framework

This application uses Minitest as the testing framework. Tests are organized by type and follow the Rails conventions.

## Running Tests

```bash
# Run all tests
bin/rails test

# Run a specific test file
bin/rails test test/models/user_test.rb

# Run a specific test
bin/rails test test/models/user_test.rb:42

# Run all model tests
bin/rails test:models

# Run all controller tests
bin/rails test:controllers

# Run all integration tests
bin/rails test:integration
```

## Example Tests

### Model Test

```ruby
require 'test_helper'

class UserTest < ActiveSupport::TestCase
  test "should not save user without email" do
    user = User.new(name: "Example User", password: "password")
    assert_not user.save, "Saved the user without an email"
  end
  
  test "should validate email format" do
    user = User.new(name: "Example User", email: "invalid", password: "password")
    assert_not user.save, "Saved the user with an invalid email"
  end
  
  test "should save valid user" do
    user = User.new(name: "Example User", email: "user@example.com", password: "password")
    assert user.save, "Could not save a valid user"
  end
end
```

### Controller Test

```ruby
require 'test_helper'

class UsersControllerTest < ActionDispatch::IntegrationTest
  setup do
    @user = users(:one)
  end
  
  test "should get index" do
    get users_url, as: :json
    assert_response :success
  end
  
  test "should create user" do
    assert_difference('User.count') do
      post users_url, params: { user: { name: "New User", email: "new@example.com", password: "password" } }, as: :json
    end
    
    assert_response :created
  end
  
  test "should show user" do
    get user_url(@user), as: :json
    assert_response :success
  end
end
```

## Fixtures

Fixtures are used to set up test data. They are defined in YAML files in the `fixtures/` directory.

### Example Fixture

```yaml
# fixtures/users.yml
one:
  name: User One
  email: one@example.com
  password_digest: <%= BCrypt::Password.create('password') %>
  admin: false
  active: true

two:
  name: User Two
  email: two@example.com
  password_digest: <%= BCrypt::Password.create('password') %>
  admin: true
  active: true
```

## Best Practices

1. Write tests for all code
2. Follow the Arrange-Act-Assert pattern
3. Keep tests focused and isolated
4. Use meaningful test names
5. Use fixtures or factories for test data
6. Test edge cases and error conditions
7. Keep tests fast and efficient
8. Maintain high test coverage
