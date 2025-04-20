# Script Directory

This directory contains utility scripts for the Rails application.

## Purpose

The script directory is used for:
- Custom utility scripts
- Deployment scripts
- Database scripts
- Data processing scripts
- Other automation scripts

## Usage

Scripts in this directory are typically run manually or as part of automated processes like CI/CD pipelines.

## Example Scripts

### Database Backup Script

```bash
#!/bin/bash
# script/backup_database.sh
# Backs up the database to S3

set -e

TIMESTAMP=$(date +%Y%m%d%H%M%S)
BACKUP_FILE="backup_$TIMESTAMP.sql"

echo "Creating database backup..."
pg_dump -U postgres app_production > $BACKUP_FILE

echo "Compressing backup..."
gzip $BACKUP_FILE

echo "Uploading to S3..."
aws s3 cp "$BACKUP_FILE.gz" "s3://app-backups/$BACKUP_FILE.gz"

echo "Cleaning up..."
rm "$BACKUP_FILE.gz"

echo "Backup complete!"
```

### Data Import Script

```ruby
#!/usr/bin/env ruby
# script/import_data.rb
# Imports data from a CSV file

require File.expand_path('../../config/environment', __FILE__)

puts "Starting data import..."

CSV.foreach('data.csv', headers: true) do |row|
  User.create!(
    name: row['name'],
    email: row['email'],
    active: row['active'] == 'true'
  )
end

puts "Import complete!"
```

## Best Practices

1. Make scripts executable (`chmod +x script/script_name.sh`)
2. Include a shebang line at the top of the script
3. Add comments explaining the script's purpose and usage
4. Handle errors appropriately
5. Use exit codes to indicate success or failure
6. Log important information
7. Make scripts idempotent when possible
8. Test scripts thoroughly

## Running Scripts

```bash
# Run a bash script
./script/backup_database.sh

# Run a Ruby script
./script/import_data.rb
```
