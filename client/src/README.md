# Source Code Directory

This directory contains all the source code for the React frontend application.

## Directory Structure

- `assets/` - Static assets like images, icons, and other media files
- `components/` - Reusable React components
- `hooks/` - Custom React hooks
- `features/` - Feature-based modules
- `utils/` - Utility functions
- `types/` - TypeScript type definitions
- `styles/` - Global styles

## Development Guidelines

### Component Structure

Components should follow a consistent structure:
- One component per file
- Use functional components with hooks
- Export as default
- Include prop types or TypeScript interfaces

Example:
```tsx
import React from 'react';

interface ButtonProps {
  label: string;
  onClick: () => void;
  disabled?: boolean;
}

const Button: React.FC<ButtonProps> = ({ label, onClick, disabled = false }) => {
  return (
    <button 
      onClick={onClick} 
      disabled={disabled}
      className="button"
    >
      {label}
    </button>
  );
};

export default Button;
```

### State Management

- Use React hooks for local state
- Consider context API for shared state
- Use Redux only for complex global state

### Code Style

- Follow the project's ESLint and Prettier configurations
- Use TypeScript for type safety
- Write meaningful comments for complex logic
- Use descriptive variable and function names
