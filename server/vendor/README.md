# Vendor Directory

This directory contains third-party code that is not managed by Bundler.

## Purpose

The vendor directory is used for:
- Third-party libraries not available as gems
- Custom versions of gems
- JavaScript libraries
- CSS libraries
- Other external code

## Usage

Code in the vendor directory is typically loaded automatically by Rails. For example, JavaScript and CSS files in the vendor directory are included in the asset pipeline.

## When to Use Vendor

Use the vendor directory when:
- A library is not available as a gem
- You need to use a custom version of a gem
- You want to include external code directly in your application

## Best Practices

1. Prefer gems over vendor files when possible
2. Document the source and version of vendor files
3. Keep vendor files up to date
4. Consider creating a gem for frequently used vendor code
5. Include license information for vendor files

## Example: Including a JavaScript Library

1. Place the library file in `vendor/assets/javascripts/`
2. Require the file in your application.js:

```javascript
//= require vendor/library-name
```

## Example: Including a CSS Library

1. Place the library file in `vendor/assets/stylesheets/`
2. Require the file in your application.css:

```css
/*
 *= require vendor/library-name
 */
```

## Documenting Vendor Files

It's important to document vendor files to make it clear where they came from and what version they are. Consider creating a README file in each vendor directory with the following information:

- Library name
- Version
- Source URL
- License
- Any modifications made
- Date added/updated
