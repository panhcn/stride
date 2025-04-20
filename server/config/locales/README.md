# Locales Directory

This directory contains internationalization (i18n) files for the Rails application.

## Purpose

The locales directory is used for:
- Storing translations for different languages
- Defining locale-specific formats for dates, numbers, etc.
- Organizing text content for easier maintenance and translation

## File Structure

Locale files are typically organized by language and/or feature:
- `en.yml` - English translations
- `fr.yml` - French translations
- `es.yml` - Spanish translations
- `en.errors.yml` - English error messages
- `en.models.yml` - English model-related translations

## Basic Usage

### Translation Files

```yaml
# config/locales/en.yml
en:
  hello: "Hello"
  welcome: "Welcome to our application"
  
  users:
    create:
      success: "User was successfully created."
      error: "Could not create user."
    update:
      success: "User was successfully updated."
      error: "Could not update user."
```

```yaml
# config/locales/fr.yml
fr:
  hello: "Bonjour"
  welcome: "Bienvenue à notre application"
  
  users:
    create:
      success: "L'utilisateur a été créé avec succès."
      error: "Impossible de créer l'utilisateur."
    update:
      success: "L'utilisateur a été mis à jour avec succès."
      error: "Impossible de mettre à jour l'utilisateur."
```

### Using Translations in Code

```ruby
# In a controller
flash[:notice] = t('users.create.success')

# In a view
<h1><%= t('welcome') %></h1>

# With variables
t('hello_name', name: user.name)

# Scoped translations
t('.success', scope: 'users.create')
```

## Advanced Features

### Pluralization

```yaml
en:
  items:
    zero: "No items"
    one: "1 item"
    other: "%{count} items"
```

```ruby
t('items', count: 0)  # => "No items"
t('items', count: 1)  # => "1 item"
t('items', count: 5)  # => "5 items"
```

### Interpolation

```yaml
en:
  welcome_message: "Welcome, %{name}!"
  items_count: "You have %{count} items in your cart."
```

```ruby
t('welcome_message', name: 'John')  # => "Welcome, John!"
t('items_count', count: 5)  # => "You have 5 items in your cart."
```

### Date and Time Formats

```yaml
en:
  time:
    formats:
      short: "%H:%M"
      default: "%a, %d %b %Y %H:%M:%S %z"
      long: "%B %d, %Y %H:%M"
  date:
    formats:
      short: "%b %d"
      default: "%Y-%m-%d"
      long: "%B %d, %Y"
```

```ruby
I18n.l(Time.now, format: :short)  # => "14:30"
I18n.l(Date.today, format: :long)  # => "April 15, 2023"
```

## Best Practices

1. Use i18n for all user-facing text
2. Organize translations logically
3. Use nested keys for better organization
4. Use variables for dynamic content
5. Keep translation keys descriptive
6. Use pluralization when appropriate
7. Test translations in all supported languages
8. Keep translations up to date
9. Consider using a translation management system for larger projects
