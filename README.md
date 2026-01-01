# @superinstance/ui

Shared React UI component library for SuperInstance applications.

## Overview

This library provides reusable, accessible, and customizable React components that are used across all SuperInstance applications. Built with:

- React 19
- TypeScript
- Tailwind CSS
- class-variance-authority for variants

## Installation

```bash
npm install @superinstance/ui
# or
yarn add @superinstance/ui
# or
pnpm add @superinstance/ui
```

## Usage

```tsx
import { Button, Card, Input } from '@superinstance/ui';
import '@superinstance/ui/styles.css';

function MyComponent() {
  return (
    <Card>
      <CardHeader>
        <CardTitle>Title</CardTitle>
      </CardHeader>
      <CardContent>
        <Input placeholder="Enter text..." />
        <Button>Submit</Button>
      </CardContent>
    </Card>
  );
}
```

## Available Components

### Form Components
- Button
- Input
- Textarea
- Select
- Checkbox
- Radio
- Switch
- Slider

### Layout Components
- Card
- Panel
- Separator
- Container

### Feedback Components
- Alert
- Toast
- Spinner
- Progress

### Navigation Components
- Tabs
- Breadcrumb
- Pagination

### Display Components
- Badge
- Avatar
- Tooltip
- Popover

## Development

```bash
# Install dependencies
pnpm install

# Build the library
pnpm build

# Watch for changes during development
pnpm dev

# Type check
pnpm type-check

# Run tests
pnpm test
```

## License

MIT

## Contributing

Contributions are welcome! Please read our contributing guidelines.
