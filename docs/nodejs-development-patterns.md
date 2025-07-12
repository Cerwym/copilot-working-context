# Node.js and TypeScript Development Preferences

Based on the Copilot Audio Notifications VS Code extension project, here are your established Node.js/TypeScript development patterns and preferences.

## Build System Preferences

### ESBuild Configuration
- **Bundler**: ESBuild for fast compilation and bundling
- **Target**: CommonJS format for Node.js compatibility
- **Production optimizations**: Minification enabled in production builds
- **Development features**: Source maps for debugging (disabled in production)
- **External dependencies**: VS Code API externalized (not bundled)
- **Custom plugins**: Problem matcher plugin for VS Code integration

### Build Scripts Architecture
```json
{
  "scripts": {
    "compile": "npm run check-types && npm run lint && node esbuild.js",
    "watch": "npm-run-all -p watch:*",
    "watch:esbuild": "node esbuild.js --watch",
    "watch:tsc": "tsc --noEmit --watch --project tsconfig.json",
    "package": "npm run check-types && npm run lint && node esbuild.js --production",
    "check-types": "tsc --noEmit",
    "lint": "eslint src"
  }
}
```

## TypeScript Configuration Patterns

### Strict Type Checking
- **noEmit**: Type checking without compilation (ESBuild handles compilation)
- **Strict mode**: Enabled for maximum type safety
- **Target**: ES2020 for modern Node.js features
- **Module resolution**: Node.js style module resolution

### Project Structure
```
src/
  ├── extension.ts          # Main entry point (standard VS Code convention)
  ├── audioService.ts       # Feature-specific services
  ├── interactionMonitor.ts # Specialized monitoring logic
  ├── commands.ts           # Command handlers
  ├── localization.ts       # i18n support
  └── test/                 # Test files co-located with source
```

## Package Management and Dependencies

### Development Dependencies Structure
- **TypeScript tooling**: `@typescript-eslint/eslint-plugin`, `@typescript-eslint/parser`
- **Build tools**: `esbuild`, `npm-run-all`
- **Testing**: `@vscode/test-cli`, `@vscode/test-electron`
- **Linting**: `eslint` with TypeScript configuration
- **VS Code tooling**: `@vscode/vsce` for extension packaging

### Dependency Organization
- **Core runtime dependencies**: Minimal, prefer built-in Node.js APIs
- **Development dependencies**: Comprehensive tooling for quality and automation
- **Platform-specific handling**: Use platform detection rather than platform-specific packages

## Semantic Versioning and Release Automation

### Automated Release Pipeline
- **semantic-release**: Fully automated versioning based on conventional commits
- **Conventional commits**: Structured commit messages for automatic changelog generation
- **GitHub Actions**: CI/CD pipeline with cross-platform testing
- **Marketplace publishing**: Automated VS Code extension publishing

### Release Configuration
```json
{
  "plugins": [
    "@semantic-release/commit-analyzer",
    "@semantic-release/release-notes-generator", 
    "@semantic-release/changelog",
    "@semantic-release/npm",
    "@semantic-release/exec",
    "@semantic-release/github",
    "@semantic-release/git"
  ]
}
```

## Code Quality and Standards

### ESLint Configuration
- **TypeScript-aware linting**: Full TypeScript ESLint integration
- **Strict rules**: Comprehensive linting for code quality
- **Pre-commit validation**: Linting integrated into build pipeline

### Development Workflow
- **Type checking**: Separate from compilation for faster iteration
- **Watch mode**: Parallel watching of TypeScript and ESBuild
- **Error handling**: Comprehensive error scenarios with proper logging
- **Testing integration**: VS Code extension testing framework

## VS Code Extension Specific Patterns

### Extension Structure
- **Activation events**: `onStartupFinished` for background services
- **Command registration**: Centralized command handler pattern
- **Configuration management**: VS Code settings integration with real-time updates
- **Internationalization**: Full i18n support with multiple language packs
- **Platform abstraction**: Cross-platform audio handling with graceful fallbacks

### Development Environment
- **Docker support**: Containerized development environment for consistency
- **VS Code workspace**: Configured settings and recommended extensions
- **Problem matchers**: Custom ESBuild problem matcher for error reporting

## Testing Approach

### Testing Philosophy
- **Headless testing**: Xvfb for Linux CI environments
- **Cross-platform**: Testing on Windows, macOS, and Linux
- **VS Code integration**: Using official VS Code testing framework
- **Automated CI**: GitHub Actions with matrix testing across platforms

### Test Configuration
- **Multiple Node versions**: Testing against Node 18 and 20
- **Multiple VS Code versions**: Testing against specific and stable versions
- **Platform matrix**: Full cross-platform test coverage

## Documentation and Project Management

### Documentation Standards
- **Comprehensive README**: Setup, configuration, and usage instructions
- **Contributing guidelines**: Conventional commit format and development workflow
- **Release notes**: Automated generation from commit messages
- **API documentation**: Inline TypeScript documentation

### Project Metadata
- **Package.json completeness**: Full metadata including sponsor links, keywords, categories
- **Marketplace optimization**: Proper categorization and keyword tagging
- **License and attribution**: Clear licensing and third-party attribution

## Performance and Production Considerations

### Build Optimization
- **Production bundling**: Minified, optimized builds for distribution
- **Source map management**: Development source maps, production without sources
- **External dependencies**: Proper externalization of runtime dependencies
- **Bundle analysis**: Clear separation of bundled vs. external code

### Runtime Performance
- **Efficient monitoring**: Event-driven architecture with minimal polling
- **Resource cleanup**: Proper disposal patterns for VS Code extensions
- **Error handling**: Graceful fallbacks and user-friendly error messages
- **Memory management**: Careful resource management for long-running extensions

## Development Tools Integration

### Git and Version Control
- **Conventional commits**: Structured commit messages for automation
- **Branch protection**: Automated protection rules via GitHub API
- **Automated workflows**: Full CI/CD with semantic versioning

### IDE Configuration
- **VS Code settings**: Workspace-specific settings for consistent development
- **Extension recommendations**: Curated list of development extensions
- **Problem matchers**: Custom matchers for build tool integration

This comprehensive Node.js/TypeScript development approach emphasizes:
- **Automation over manual processes**
- **Type safety throughout the development lifecycle**
- **Cross-platform compatibility from the start**
- **Professional release management with semantic versioning**
- **Comprehensive testing and quality assurance**
- **Clean architecture with proper separation of concerns**

These patterns reflect a mature, professional Node.js development workflow suitable for open-source projects and enterprise applications.
