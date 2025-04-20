# Controllers Directory

This directory contains controller classes that handle HTTP requests and responses.

## Purpose

Controllers are responsible for:
- Receiving HTTP requests
- Processing input parameters
- Interacting with models and services
- Rendering responses (JSON for API endpoints)

## Structure

- Base controllers (ApplicationController, etc.)
- Resource-specific controllers
- API versioned controllers (if applicable)
- `concerns/` directory for shared functionality

## Best Practices

### Controller Design

1. Keep controllers thin
   - Move complex business logic to service objects
   - Use models for data access and validation

2. Follow RESTful conventions
   - Use standard CRUD actions (index, show, create, update, destroy)
   - Use appropriate HTTP verbs and status codes

3. Parameter handling
   - Use strong parameters for security
   - Validate input early

4. Error handling
   - Use consistent error response format
   - Handle exceptions gracefully

### Example Controller

```ruby
# typed: strict
class UsersController < ApplicationController
  extend T::Sig
  
  sig { void }
  def index
    @users = User.active
    render json: @users
  end
  
  sig { void }
  def show
    @user = User.find(params[:id])
    render json: @user
  rescue ActiveRecord::RecordNotFound
    render json: { error: 'User not found' }, status: :not_found
  end
  
  sig { void }
  def create
    @user = User.new(user_params)
    
    if @user.save
      render json: @user, status: :created
    else
      render json: { errors: @user.errors }, status: :unprocessable_entity
    end
  end
  
  private
  
  sig { returns(T::Hash[Symbol, T.untyped]) }
  def user_params
    params.require(:user).permit(:name, :email, :password)
  end
end
```
