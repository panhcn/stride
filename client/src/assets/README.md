# Assets Directory

This directory contains static assets used in the application.

## Contents

- Images
- Icons
- Fonts
- Other media files

## Usage Guidelines

### Importing Assets

Assets can be imported directly in React components:

```tsx
import logo from '../assets/logo.png';

const Header = () => {
  return (
    <header>
      <img src={logo} alt="Logo" />
    </header>
  );
};
```

### Asset Organization

- Group assets by type (images, icons, etc.)
- Use descriptive filenames
- Consider using subdirectories for better organization
- Optimize images and other assets for web use

### Best Practices

1. Use SVG for icons and simple graphics when possible
2. Optimize images before adding them to the project
3. Consider using WebP format for better compression
4. Include appropriate alt text when using images in components
5. Use lazy loading for non-critical images
