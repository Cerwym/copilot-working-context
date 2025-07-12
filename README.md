# Copilot Working Context

##  **Working Style Preferences**
- **Detailed explanations**: Always explain what we're doing and why
- **Comprehensive commit messages**: Include achievements, impact, and technical details
- **Quality metrics**: Show test counts, compilation status, and performance
- **Phase-based approach**: Break large features into logical phases
- **Clean architecture**: Prefer abstractions, dependency injection, and testability
- **Documentation-driven**: Keep GitHub issues updated with progress

##  **Testing Approach**
- **Test isolation**: Prefer in-memory providers over file system dependencies
- **Comprehensive coverage**: Test happy path, edge cases, and error scenarios
- **Quality gates**: All tests must pass before committing
- **Mock patterns**: Use dependency injection to enable clean mocking

##  **Progress Tracking**
- **GitHub issues**: Use for feature roadmaps and progress tracking
- **Commit messages**: Detailed with impact metrics (test counts, warnings, etc.)
- **Branch naming**: Feature branches with descriptive names
- **Documentation**: Keep README and inline docs up to date

##  **Technical Preferences**
- **C# .NET**: Prefer nullable reference types, clean architecture
- **Platform abstractions**: Write portable code that avoids platform lock-in
- **Cross-platform compatibility**: Ensure code works on Windows, macOS, and Linux
- **Line endings**: Unix-style (LF) with Git autocrlf=input to prevent cross-platform issues
- **Documentation**: Mermaid diagrams for visual architecture representation
- **JiraTools integration**: Use custom JiraTools CLI for workflow automation and story management
- **Abstraction layers**: Use interfaces and dependency injection for platform-specific features
- **Error handling**: Comprehensive error scenarios with logging
- **Performance**: Always consider performance implications
- **Backwards compatibility**: Maintain during refactoring

##  **Project Patterns**
- **Configuration**: Provider pattern for testability
- **Commands**: Dependency injection with interfaces
- **Testing**: Organized by logical areas (Commands/, Core/, etc.)
- **Documentation**: Inline XML docs for public APIs

##  **Repository Architecture**
- **Modular separation**: Use Git submodules to separate context documentation from implementations
- **Independent versioning**: Core preferences (this repo) vs. tool implementations (submodules)
- **Clean boundaries**: Context definitions remain stable while implementations evolve independently
- **Reusable components**: Tools can be shared across different context repositories
- **Development workflow**: Update context preferences here, develop/test tools in their own repos
- **Multi-tool support**: VS Code extensions (vs-code-extensions/) and CLI tools (jira-tools/)

---
*Last updated: July 12, 2025*
*Use this context to maintain consistency across different machines and projects*
