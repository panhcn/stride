# Client (React Application)

## Directory Structure
client/
├── src/        # Source code
│   ├── components/    # React components
│   ├── hooks/        # Custom React hooks
│   ├── features/     # Feature-based modules
│   ├── utils/        # Utility functions
│   ├── types/        # TypeScript type definitions
│   └── styles/       # Global styles
├── public/     # Static assets
├── tests/      # Test files
└── dist/       # Production build output

## File Naming Conventions
- Components: `PascalCase.tsx`
- Hooks: `useCamelCase.ts`
- Utils: `camelCase.ts`
- Constants: `SCREAMING_SNAKE_CASE.ts`
- Styles: `PascalCase.css` or `PascalCase.module.css`
- Tests: `PascalCase.test.tsx`

## Testing

### Test File Organization
```
tests/
├── components/         # Component tests
├── hooks/             # Hook tests
├── features/          # Feature module tests
├── utils/             # Utility function tests
├── integration/       # Integration tests
└── setup/             # Test setup and configuration
```

### Core Testing Requirements
1. Component Tests
   - Test rendering
   - Test user interactions
   - Test prop variations
   - Test error states

2. Hook Tests
   - Test all possible states
   - Test side effects
   - Test cleanup

3. Integration Tests
   - Test feature workflows
   - Test component interactions
   - Test data flow

### Coverage Requirements
- Line Coverage: Minimum 95%
- Branch Coverage: Minimum 95%
- Function Coverage: Minimum 95%

### Running Tests
```bash
# Run all tests
npm test

# Run tests in watch mode
npm test -- --watch

# Run with coverage
npm test -- --coverage
```

### Test Categories Required
1. Component Rendering
2. User Interactions
3. State Management
4. API Integration
5. Error Handling
6. Form Validation
7. Routing
8. Authentication Flow
9. Performance
10. Accessibility

### Best Practices
1. Use React Testing Library
2. Focus on user behavior
3. Avoid implementation details
4. Mock API calls
5. Use meaningful test descriptions
6. Test accessibility
7. Keep tests isolated
8. Use proper cleanup

### Type Checking
- Use TypeScript in strict mode
- No `any` types in new code
- Props and state must be fully typed
- Use proper type imports from React
