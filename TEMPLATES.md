# Copilot Templates

##  **Quick Start Commands**

### For new C# projects:
\\\
Please read my working context at: https://github.com/Cerwym/copilot-working-context
Create a new .NET 8.0 console application with:
- Nullable reference types enabled
- Clean architecture with dependency injection
- Comprehensive test coverage with xUnit
- Cross-platform compatibility
\\\

### For existing project analysis:
\\\
Please read my working context at: https://github.com/Cerwym/copilot-working-context
Analyze this project and suggest improvements following my architectural preferences:
- Configuration provider patterns
- Test isolation with in-memory providers
- Platform abstraction layers
\\\

##  **Commit Message Template**
\\\
feat(area): Brief description of change

- Key achievement/impact
- Technical details
- Tests: X passing, Y added
- Warnings: None/Resolved
- Performance: Impact description

Addresses #issue-number
\\\

##  **Branch Naming Convention**
\\\
Before starting work, create appropriately prefixed branches:
- **feature/**: New features or enhancements
- **bugfix/**: Bug fixes and corrections
- **misc/**: Miscellaneous work, refactoring, documentation

Branch names should reference Jira story when applicable:
- feature/PROJ-123-implement-user-authentication
- bugfix/PROJ-456-fix-memory-leak
- misc/update-documentation

**Note**: This rule can be relaxed for personal/non-company work
\\\

##  **Development Workflow Template**
\\\
When starting new development work:

1. **Check for Jira Story**:
   - Is this company work? If yes, ensure Jira story exists
   - If no Jira story exists, offer to create one using JiraTools application
   - For personal projects, Jira requirement can be waived

**JiraTools Commands:**
```bash
# Navigate to JiraTools submodule directory
cd jira-tools

# Create a new task
dotnet run -- create-task --summary "Task title" --description "Detailed description" --type "Task" --components "ComponentName"

# Create task linked to parent (uses default parent from .env)
dotnet run -- create-task --summary "Task title" --description "Description" --parent

# Check task status and available transitions
dotnet run -- workflow-help --issue-key PROJ-12345

# Transition task through complete workflow
dotnet run -- complete --issue-key PROJ-12345 --target "Done" --non-interactive
```

2. **Create Branch**:
   - Use appropriate prefix: feature/, bugfix/, or misc/
   - Include Jira ID if applicable: feature/PROJ-123-description
   - For personal work: feature/descriptive-name

3. **Development Process**:
   - Follow clean architecture principles
   - Maintain comprehensive test coverage
   - Use detailed commit messages with impact metrics

4. **Integration**:
   - Ensure all tests pass
   - Update documentation as needed
   - Reference Jira story in PR/commit if applicable
\\\

##  **Test Structure Template**
\\\csharp
[Fact]
public void MethodName_WhenCondition_ShouldExpectedOutcome()
{
    // Arrange
    var mockDependency = new Mock<IDependency>();
    var sut = new SystemUnderTest(mockDependency.Object);

    // Act
    var result = sut.MethodToTest();

    // Assert
    Assert.NotNull(result);
    mockDependency.Verify(x => x.ExpectedCall(), Times.Once);
}
\\\

##  **Configuration Provider Pattern**
\\\csharp
public interface IConfigurationProvider<T>
{
    Task<T> GetConfigurationAsync();
    Task SaveConfigurationAsync(T configuration);
}

public class InMemoryConfigurationProvider<T> : IConfigurationProvider<T>
{
    private T? _configuration;

    public Task<T> GetConfigurationAsync()
        => Task.FromResult(_configuration ?? throw new InvalidOperationException());

    public Task SaveConfigurationAsync(T configuration)
    {
        _configuration = configuration;
        return Task.CompletedTask;
    }
}
\\\

---
*Use these templates to maintain consistency and speed up development*
