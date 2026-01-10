# Contributing to @superinstance/ui

Thank you for your interest in contributing to @superinstance/ui! This package provides shared React UI components for SuperInstance applications.

## Table of Contents

- [Quick Start](#quick-start)
- [Development Environment Setup](#development-environment-setup)
- [Development Workflow](#development-workflow)
- [Code Standards](#code-standards)
- [Testing Guidelines](#testing-guidelines)
- [Component Guidelines](#component-guidelines)
- [Documentation Standards](#documentation-standards)
- [Submitting Changes](#submitting-changes)
- [Getting Help](#getting-help)

---

## Quick Start

```bash
# Clone the repository
git clone https://github.com/SuperInstance/UI.git
cd UI

# Install dependencies
pnpm install

# Start development mode
pnpm dev

# Make your changes
# ... edit files ...

# Run tests and linting
pnpm test
pnpm lint
pnpm type-check

# Submit a pull request
```

---

## Development Environment Setup

### Prerequisites

**Required:**
- Node.js 18+ (20+ recommended)
- pnpm 8+ (package manager)
- Git 2.30+

**Recommended:**
- 4GB+ RAM
- Modern web browser (for development)
- VS Code with recommended extensions

### Installation

```bash
# Fork the repository on GitHub first
# Then clone your fork
git clone https://github.com/YOUR_USERNAME/UI.git
cd UI

# Install dependencies
pnpm install

# Run the development build
pnpm dev

# Verify setup by running tests
pnpm test
```

### IDE Configuration

**VS Code (Recommended):**

Install these extensions:
- ESLint
- Prettier
- TypeScript and JavaScript Language Features

Configure workspace settings (`.vscode/settings.json`):
```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "typescript.tsdk": "node_modules/typescript/lib"
}
```

---

## Development Workflow

### Finding Something to Work On

- Check [GitHub Issues](https://github.com/SuperInstance/UI/issues) for open tasks
- Look for labels: `good first issue`, `help wanted`, `component`, `enhancement`
- Review the component roadmap
- Comment on the issue to claim it

### Creating a Branch

```bash
# Ensure you're on main and up to date
git checkout main
git pull origin main

# Create a feature branch
git checkout -b feat/component-name

# Or a bug fix branch
git checkout -b fix/issue-number-brief-description

# Branch naming conventions:
# feat/ - New features or components
# fix/ - Bug fixes
# docs/ - Documentation changes
# chore/ - Maintenance tasks
# style/ - Visual/styling changes
```

### Making Changes

- Write code following our [Code Standards](#code-standards)
- Add tests for new functionality (see [Testing Guidelines](#testing-guidelines))
- Update documentation as needed
- Keep commits atomic and well-described

### Commit Messages

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
type(scope): description

[optional body]
```

**Types:**
- `feat` - New features or components
- `fix` - Bug fixes
- `docs` - Documentation changes
- `style` - Code style changes (formatting, no logic change)
- `refactor` - Code refactoring
- `test` - Adding or updating tests
- `chore` - Maintenance tasks

**Examples:**
```bash
git commit -m "feat(button): add loading state support"
git commit -m "fix(modal): resolve z-index stacking issue"
git commit -m "docs(readme): update installation instructions"
```

---

## Code Standards

### TypeScript Guidelines

**General Principles:**
- Use strict TypeScript settings
- Prefer explicit types over `any`
- Use interfaces for public APIs
- Add JSDoc comments for exports

**Naming Conventions:**
```typescript
// Components: PascalCase
export function Button({ }: ButtonProps) { }
export const Card: React.FC<CardProps> = ({ }) => { };

// Functions: camelCase
export function formatDate(date: Date): string { }

// Constants: UPPER_SNAKE_CASE
export const MAX_HEIGHT = 500;

// Types/Interfaces: PascalCase
export interface ButtonProps { }
export type ColorVariant = 'primary' | 'secondary';

// Props interfaces: ComponentName + Props
export interface ButtonProps { }
export interface ModalProps { }
```

**Code Style:**
- 2 space indentation
- Single quotes for strings
- Semicolons required
- Max line length: 100
- No trailing whitespace
- Use `React.FC` for function components (optional)

```typescript
// Good
export const Button: React.FC<ButtonProps> = ({
  children,
  variant = 'primary',
  disabled = false,
  onClick,
}) => {
  const handleClick = (e: React.MouseEvent) => {
    if (!disabled) {
      onClick?.(e);
    }
  };

  return (
    <button
      className={cn(styles.button, styles[variant])}
      disabled={disabled}
      onClick={handleClick}
    >
      {children}
    </button>
  );
};
```

### CSS/Tailwind Guidelines

- Use Tailwind utility classes
- Use `cn()` helper for conditional classes
- Use `class-variance-authority` for variants
- Keep component-scoped styles separate

```typescript
import { cn } from '@superinstance/ui/lib/utils';

export const Button = ({ className, variant, ...props }) => {
  return (
    <button
      className={cn(
        'base-classes',
        variant === 'primary' && 'primary-classes',
        className
      )}
      {...props}
    />
  );
};
```

### Import Order

```typescript
// 1. React
import React, { useState, useEffect } from 'react';

// 2. External dependencies
import { clsx } from 'clsx';
import { twMerge } from 'tailwind-merge';

// 3. Internal imports
import { Button } from './Button';
import { useStyles } from './Button.styles';

// 4. Types
import type { ButtonProps } from './Button.types';
```

---

## Testing Guidelines

### Running Tests

```bash
# Run all tests
pnpm test

# Run tests in watch mode
pnpm test --watch

# Run tests with coverage
pnpm test --coverage

# Run specific test file
pnpm test Button.test.tsx
```

### Writing Tests

Use Vitest for unit testing:

```typescript
import { render, screen } from '@testing-library/react';
import { describe, it, expect, vi } from 'vitest';
import { Button } from './Button';

describe('Button', () => {
  it('renders children correctly', () => {
    render(<Button>Click me</Button>);
    expect(screen.getByText('Click me')).toBeInTheDocument();
  });

  it('calls onClick when clicked', () => {
    const handleClick = vi.fn();
    render(<Button onClick={handleClick}>Click me</Button>);

    screen.getByText('Click me').click();
    expect(handleClick).toHaveBeenCalledTimes(1);
  });

  it('is disabled when disabled prop is true', () => {
    render(<Button disabled>Click me</Button>);
    expect(screen.getByRole('button')).toBeDisabled();
  });
});
```

### Test Coverage Goals

- **Critical components**: 90%+ coverage
- **Standard components**: 70%+ coverage
- **Utility functions**: 80%+ coverage

---

## Component Guidelines

### Component Structure

```
src/
├── components/
│   ├── button/
│   │   ├── Button.tsx           # Main component
│   │   ├── Button.test.tsx      # Tests
│   │   ├── Button.types.ts      # Type definitions
│   │   ├── index.ts             # Export barrel
```

### Component Checklist

When adding a new component:

1. **Requirements**
   - [ ] Component has a clear purpose
   - [ ] Follows existing component patterns
   - [ ] Has proper TypeScript types
   - [ ] Supports dark mode
   - [ ] Ensures accessibility (ARIA attributes)

2. **Implementation**
   - [ ] Code follows style guidelines
   - [ ] Uses existing utilities (cn, cva)
   - [ ] Handles edge cases
   - [ ] Has appropriate error handling

3. **Testing**
   - [ ] Unit tests cover main functionality
   - [ ] Tests cover edge cases
   - [ ] Tests for accessibility

4. **Documentation**
   - [ ] JSDoc comments for props
   - [ ] Usage examples
   - [ ] Story (if using Storybook)

### Accessibility

Components must be accessible:

```typescript
// Good - accessible button
<button
  type="button"
  disabled={disabled}
  aria-label={ariaLabel}
  aria-describedby={descriptionId}
>
  {children}
</button>

// Good - accessible form input
<label htmlFor={id}>{label}</label>
<input
  id={id}
  type={type}
  aria-invalid={hasError}
  aria-describedby={errorId}
/>
{hasError && <span id={errorId}>{error}</span>}
```

---

## Documentation Standards

### JSDoc Comments

Every exported component/function must have JSDoc:

```typescript
/**
 * Button component with support for variants and sizes.
 *
 * @example
 * ```tsx
 * <Button variant="primary" size="md">
 *   Click me
 * </Button>
 * ```
 */
export const Button: React.FC<ButtonProps> = (props) => {
  // ...
};
```

### README

Each component directory should have documentation:

```markdown
# Button

A clickable button component with support for variants and sizes.

## Usage

```tsx
import { Button } from '@superinstance/ui';

<Button variant="primary">Click me</Button>
```

## API

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| variant | `'primary' \| 'secondary'` | `'primary'` | Visual style variant |
| size | `'sm' \| 'md' \| 'lg'` | `'md'` | Button size |
| disabled | `boolean` | `false` | Disable the button |
```

---

## Submitting Changes

### Before Submitting

- [ ] Code follows style guidelines
- [ ] Tests pass locally (`pnpm test`)
- [ ] Linting passes (`pnpm lint`)
- [ ] Type checking passes (`pnpm type-check`)
- [ ] Build succeeds (`pnpm build`)
- [ ] Documentation updated
- [ ] New tests added for features

### Creating the Pull Request

1. **Push your branch**:
   ```bash
   git push origin feat/component-name
   ```

2. **Create PR on GitHub**:
   - Go to https://github.com/SuperInstance/UI
   - Click "New Pull Request"
   - Select your branch
   - Fill out the PR template

3. **PR Template**:
   ```markdown
   ## Description
   Brief description of the component or changes

   ## Type of Change
   - [ ] New component
   - [ ] Bug fix
   - [ ] Enhancement
   - [ ] Breaking change
   - [ ] Documentation

   ## Component Changes
   - What components were added/modified
   - What new features were added

   ## Testing
   - [ ] Tests added/updated
   - [ ] All tests passing
   - [ ] Accessibility tested

   ## Screenshots
   (For UI changes) Add screenshots

   ## Checklist
   - [ ] Code follows style guidelines
   - [ ] Self-review performed
   - [ ] Documentation updated
   - [ ] No new linting errors
   ```

### During Review

- Respond to feedback promptly
- Make requested changes
- Push updates to the same branch
- Ask questions if anything is unclear

---

## Getting Help

### Documentation

- [README.md](README.md) - Package overview
- [Component Docs](./docs/) - Component documentation
- [Type Definitions](./dist/index.d.ts) - API reference

### Community Resources

- **GitHub Issues**: Bug reports and feature requests
- **GitHub Discussions**: Questions and ideas
- **Email**: dev@superinstance.ai

### Asking Good Questions

Before asking, please:

1. **Search first**: Check existing issues and docs
2. **Be specific**: Include code snippets, error messages
3. **Provide context**: What you're trying to do
4. **Format code**: Use markdown code blocks
5. **Include reproduction**: Minimal reproduction for bugs

---

## Recognition

We value all contributions! Contributors will be:

- Listed in CONTRIBUTORS.md
- Mentioned in release notes for significant contributions
- Eligible for contributor badges

Thank you for contributing to @superinstance/ui!

---

*Last Updated: 2026-01-10*
