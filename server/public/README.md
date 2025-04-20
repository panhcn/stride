# Public Directory

This directory contains static files that are served directly by the Rails application.

## Purpose

The public directory is used for:
- Static assets
- Error pages
- Robots.txt
- Favicon
- Other files that should be directly accessible

## Common Files

- `404.html` - Not Found error page
- `422.html` - Unprocessable Entity error page
- `500.html` - Internal Server Error page
- `robots.txt` - Instructions for web crawlers
- `favicon.ico` - Website icon

## Usage

Files in this directory are served directly by the web server, bypassing the Rails application. This makes them ideal for:
- Error pages that need to be displayed when the application is down
- Files that need to be accessible by web crawlers
- Static assets that don't need to be processed

## Best Practices

1. Keep the public directory clean and organized
2. Use asset pipeline or webpacker for application assets
3. Customize error pages to match your application's design
4. Configure robots.txt appropriately for your application
5. Consider using a CDN for serving static assets in production

## Example robots.txt

```
# Allow all crawlers
User-agent: *
Allow: /

# Disallow admin area
Disallow: /admin/

# Sitemap location
Sitemap: https://example.com/sitemap.xml
```

## Example Custom Error Page

```html
<!DOCTYPE html>
<html>
<head>
  <title>Page Not Found (404)</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <style>
  .error-page {
    background-color: #EFEFEF;
    color: #2E2F30;
    text-align: center;
    font-family: arial, sans-serif;
    margin: 0;
  }

  .error-page div.dialog {
    width: 95%;
    max-width: 33em;
    margin: 4em auto 0;
  }

  .error-page h1 {
    font-size: 100%;
    color: #730E15;
    line-height: 1.5em;
  }
  </style>
</head>

<body class="error-page">
  <div class="dialog">
    <div>
      <h1>The page you were looking for doesn't exist.</h1>
      <p>You may have mistyped the address or the page may have moved.</p>
    </div>
    <p>If you are the application owner check the logs for more information.</p>
  </div>
</body>
</html>
```
