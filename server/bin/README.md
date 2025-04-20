# Bin Directory

This directory contains executable scripts for the Rails application.

## Purpose

The bin directory contains scripts that are used to:
- Start the Rails server
- Run the Rails console
- Execute rake tasks
- Run tests
- Set up the application
- Other utility scripts

## Common Scripts

- `rails` - The main Rails command
- `rake` - For running Rake tasks
- `setup` - For setting up the application
- `bundle` - For managing gems
- `yarn` - For managing JavaScript packages
- `spring` - For application preloading

## Usage

Most scripts can be run directly from the command line:

```bash
# Start the Rails server
bin/rails server

# Run the Rails console
bin/rails console

# Run migrations
bin/rails db:migrate

# Run tests
bin/rails test
```

## Custom Scripts

You can add custom scripts to this directory to automate common tasks. Make sure to:
1. Make the script executable (`chmod +x bin/script_name`)
2. Include a shebang line at the top of the script (e.g., `#!/usr/bin/env ruby`)
3. Document the script's purpose and usage

## Best Practices

1. Use the scripts in the bin directory instead of running commands directly
2. Keep scripts focused on a single task
3. Document scripts thoroughly
4. Make sure scripts are executable
5. Use appropriate error handling in scripts
