# Contributing to @superinstance/ui

Thank you for your interest in contributing!

## How to Contribute

### Reporting Issues

Found a bug? Have a feature request? Please open an issue on GitHub.

### Submitting Pull Requests

1. Fork the repository
2. Create your feature branch (`git checkout -b feat/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feat/amazing-feature`)
5. Open a Pull Request

### Commit Message Conventions

We use [Conventional Commits](https://www.conventionalcommits.org/):

- `feat:` - New features
- `fix:` - Bug fixes
- `docs:` - Documentation changes
- `style:` - Code style changes (formatting, etc.)
- `refactor:` - Code refactoring
- `test:` - Adding or updating tests
- `chore:` - Maintenance tasks

### Development Setup

```bash
git clone https://github.com/YOUR_USERNAME/UI.git
cd UI
pnpm install
pnpm dev
```

### Coding Standards

- Use TypeScript for all new code
- Follow existing code style
- Add JSDoc comments for exports
- Test your changes before submitting

### Component Guidelines

When adding components:

1. Keep them simple and composable
2. Use proper TypeScript types
3. Support dark mode
4. Ensure accessibility (ARIA attributes)
5. Add examples in the README

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
