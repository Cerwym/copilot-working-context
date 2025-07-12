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
