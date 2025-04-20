# Database Directory

This directory contains database-related files for the Rails application.

## Purpose

The db directory contains files related to:
- Database schema
- Migrations
- Seeds
- Database configuration

## Directory Structure

- `migrate/` - Database migration files
- `schema.rb` - Current database schema
- `seeds.rb` - Seed data for the database

## Migrations

Migrations are used to modify the database schema over time. They are stored in the `migrate/` directory and are named with a timestamp and a description of the change.

### Creating Migrations

```bash
# Create a new migration
bin/rails generate migration CreateUsers
```

### Example Migration

```ruby
class CreateUsers < ActiveRecord::Migration[7.0]
  def change
    create_table :users do |t|
      t.string :name, null: false
      t.string :email, null: false
      t.string :password_digest, null: false
      t.boolean :admin, default: false
      t.boolean :active, default: true
      
      t.timestamps
    end
    
    add_index :users, :email, unique: true
  end
end
```

### Running Migrations

```bash
# Run pending migrations
bin/rails db:migrate

# Rollback the last migration
bin/rails db:rollback

# Rollback multiple migrations
bin/rails db:rollback STEP=3

# Reset the database
bin/rails db:reset
```

## Seeds

The `seeds.rb` file is used to populate the database with initial data.

### Example Seeds

```ruby
# Create admin user
User.create!(
  name: 'Admin User',
  email: 'admin@example.com',
  password: 'password',
  admin: true
)

# Create regular users
5.times do |i|
  User.create!(
    name: "User #{i}",
    email: "user#{i}@example.com",
    password: 'password'
  )
end
```

### Running Seeds

```bash
# Run seeds
bin/rails db:seed

# Reset database and run seeds
bin/rails db:reset
```

## Best Practices

1. Keep migrations small and focused
2. Use reversible migrations when possible
3. Add appropriate indexes for performance
4. Use foreign key constraints for data integrity
5. Document complex migrations
6. Keep seed data realistic and useful for development
7. Use transactions in migrations for safety
