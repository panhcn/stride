# Model Concerns Directory

This directory contains modules that can be included in models to share functionality.

## Purpose

Model concerns are used to:
- Extract and share common functionality between models
- Keep models DRY (Don't Repeat Yourself)
- Organize cross-cutting concerns like state machines, tagging, etc.

## Best Practices

### When to Use Concerns

Use concerns when:
- Multiple models need the same functionality
- A model is getting too large and complex
- Functionality is distinct and can be isolated

### Structure of a Concern

```ruby
# typed: strict
module Taggable
  extend ActiveSupport::Concern
  extend T::Sig
  
  included do
    has_many :taggings, as: :taggable, dependent: :destroy
    has_many :tags, through: :taggings
  end
  
  # Class methods
  class_methods do
    sig { params(tag_name: String).returns(T::ActiveRecord_Relation) }
    def with_tag(tag_name)
      joins(:tags).where(tags: { name: tag_name })
    end
  end
  
  # Instance methods
  sig { params(tag_names: T::Array[String]).void }
  def add_tags(tag_names)
    tag_names.each do |name|
      tag = Tag.find_or_create_by(name: name)
      tags << tag unless tags.include?(tag)
    end
  end
  
  sig { returns(T::Array[String]) }
  def tag_list
    tags.map(&:name)
  end
end
```

### Implementation Example

```ruby
# In a model
class Article < ApplicationRecord
  include Taggable
  
  # This model now has tagging functionality
end
```

## Common Concerns

- Searchable
- Sortable
- Filterable
- Taggable
- Publishable
- Archivable
- Sluggable
- Versionable

## Type Safety

As with all code in the application:
- Use `# typed: strict` or higher
- Include full type signatures
- Test thoroughly
