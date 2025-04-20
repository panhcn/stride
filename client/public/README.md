# Public Directory

This directory contains static files that are served directly without being processed by the build system.

## Contents

- `index.html` - The HTML template for the application
- Favicon and other browser icons
- Robots.txt
- Manifest files
- Static assets that need to be referenced by absolute URL

## Usage Guidelines

### When to Use Public Directory

Use this directory for:
- Files that need to be referenced by their exact filename in the built output
- Files that need to be accessible by a specific URL path
- Assets that don't need to be processed by the build system

### When Not to Use Public Directory

Don't use this directory for:
- Assets that are imported directly by your JavaScript/TypeScript code
- CSS, SCSS, or other stylesheets that are imported by your code
- Images that are used in your components

### Best Practices

1. Keep the public directory clean and organized
2. Only include files that truly need to be served as static assets
3. Consider using the `src/assets` directory for files that are imported by your code
4. Update the `index.html` file carefully, as it's the entry point for your application
