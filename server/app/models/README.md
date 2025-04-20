# Models Directory

This directory contains ActiveRecord model classes that represent database tables and business logic.

## Purpose

Models are responsible for:
- Representing database tables and relationships
- Implementing business logic and validation rules
- Providing an interface for data access and manipulation

## Structure

- Base models (ApplicationRecord, etc.)
- Domain-specific models
- `concerns/` directory for shared functionality

## Best Practices

### Model Design

1. Single Responsibility
   - Each model should represent a single concept
   - Extract complex logic to service objects when appropriate

2. Validations
   - Include all necessary validations
   - Use custom validators for complex rules

3. Associations
   - Define all relationships clearly
   - Use appropriate association types

4. Scopes
   - Use scopes for common queries
   - Keep scope definitions clear and focused

### Example Model

```ruby
# typed: strict
class User < ApplicationRecord
  extend T::Sig
  
  # Associations
  has_many :posts, dependent: :destroy
  has_one :profile, dependent: :destroy
  belongs_to :team, optional: true
  
  # Validations
  validates :email, presence: true, uniqueness: true, format: { with: URI::MailTo::EMAIL_REGEXP }
  validates :username, presence: true, uniqueness: true, length: { minimum: 3, maximum: 30 }
  
  # Scopes
  scope :active, -> { where(active: true) }
  scope :admins, -> { where(admin: true) }
  
  # Instance methods
  sig { returns(String) }
  def full_name
    "#{first_name} #{last_name}"
  end
  
  sig { returns(T::Boolean) }
  def active_admin?
    active? && admin?
  end
  
  # Class methods
  sig { params(email: String).returns(T.nilable(User)) }
  def self.find_by_email(email)
    find_by(email: email)
  end
end
```

## Type Safety

As specified in the server README, type safety is enforced:
- Models must be `# typed: strict` minimum
- Full type signatures required
- No `T.untyped` in public APIs
- Test coverage with types
