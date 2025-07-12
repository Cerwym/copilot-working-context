# Coding Style Preferences

This document outlines coding style and architectural preferences to be followed when working on projects in this repository.

## TypeScript/JavaScript Style Preferences

### Conditional Statements

#### Ternary Operators for Simple Conditions
**Preference**: Use ternary operators for simple if/else statements rather than full if blocks.

**Examples:**

 **Preferred:**
`	ypescript
// Simple assignment
const message = isEnabled ? 'Enabled' : 'Disabled';

// Simple function calls
currentlyEnabled ? await handleDisableCommand() : await handleEnableCommand();

// Simple guard clauses with null
monitor ? monitor.stopMonitoring() : null;

// Simple console logging
error ? console.warn('Failed to set volume:', error.message) : null;
stderr ? console.warn(Audio stderr: ) : null;
`

 **Avoid for simple cases:**
`	ypescript
// Don't use full if blocks for simple assignments
if (isEnabled) {
    message = 'Enabled';
} else {
    message = 'Disabled';
}

// Don't use full if blocks for simple function calls
if (currentlyEnabled) {
    await handleDisableCommand();
} else {
    await handleEnableCommand();
}

// Don't use full if blocks for simple guard clauses
if (monitor) {
    monitor.stopMonitoring();
}
`

#### When to Use Traditional If Statements
Use traditional if statements for:
- Complex logic with multiple lines
- Early returns that exit functions
- Multiple nested conditions
- Error handling with multiple operations
- When readability would be compromised

**Examples:**
`	ypescript
// Complex logic - use traditional if
if (!this.audioService.isEnabled()) {
    vscode.window.showWarningMessage(l10n('commands.testSound.disabled'));
    return;
}

// Multiple operations - use traditional if
if (audioService.isEnabled()) {
    if (!monitor) {
        console.log('Monitor not initialized, skipping start');
        return;
    }
    monitor.clearPendingState();
    monitor.startMonitoring();
} else {
    monitor ? monitor.stopMonitoring() : null;
}
`

### Clean Architecture Principles

#### Module Organization
- **Single Responsibility**: Each module should have one clear purpose
- **Focused Files**: Keep files under 200-300 lines when possible
- **Service-Oriented**: Extract functionality into focused service classes
- **Dependency Injection**: Pass dependencies through constructors

#### File Structure Preferences
`
src/
 extension.ts          # Entry point, service orchestration only
 services/
    audioService.ts   # Audio functionality
    monitorService.ts # Interaction monitoring
    localizationService.ts # Internationalization
 commands/
    commandHandlers.ts # Command registration and handling
 types/
     interfaces.ts     # Type definitions
`

### Error Handling
- Use ternary operators for simple error logging
- Use traditional try/catch for complex error handling
- Prefer explicit null checks over implicit ones

### Naming Conventions
- Use descriptive, clear names
- Prefer explicit over abbreviated names
- Use consistent naming patterns across similar functions

## Implementation Notes

These preferences prioritize:
1. **Readability** - Code should be easy to understand at a glance
2. **Conciseness** - Avoid unnecessary verbosity for simple operations
3. **Consistency** - Use the same patterns throughout the codebase
4. **Maintainability** - Code should be easy to modify and extend

## Examples from Recent Work

### Commands Module Refactoring
`	ypescript
// Simple toggle logic using ternary
private async handleToggleCommand(): Promise<void> {
    const currentlyEnabled = this.audioService.isEnabled();
    currentlyEnabled ? await this.handleDisableCommand() : await this.handleEnableCommand();
}

// Complex status display using traditional if with ternary for simple parts
private handleShowStatusCommand(): void {
    const isEnabled = this.audioService.isEnabled();
    const activeOpsCount = this.monitor.activeOperationsCount;
    const activeOps = this.monitor.activeOperationsList;
    
    let message = isEnabled ? 
        l10n('commands.showStatus.enabled') : 
        l10n('commands.showStatus.disabled');
    
    activeOpsCount > 0 ? (
        message += '\n' + l10n('commands.showStatus.activeOperations', activeOpsCount.toString()),
        activeOps.length > 0 ? message += '\n' + activeOps.join(', ') : null
    ) : null;
    
    vscode.window.showInformationMessage(message, { modal: false });
}
`

---

*Last Updated: July 12, 2025*
*Context: VS Code Extensions, TypeScript, Clean Architecture*
