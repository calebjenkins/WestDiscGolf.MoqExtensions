# MoqExtensions
[![.github/workflows/ci.yml](https://github.com/calebjenkins/WestDiscGolf.MoqExtensions/actions/workflows/ci.yml/badge.svg)](https://github.com/calebjenkins/WestDiscGolf.MoqExtensions/actions/workflows/ci.yml) 
[![.github/workflows/ci-main-deploy.yml](https://github.com/calebjenkins/WestDiscGolf.MoqExtensions/actions/workflows/ci-main-deploy.yml/badge.svg)](https://github.com/calebjenkins/WestDiscGolf.MoqExtensions/actions/workflows/ci-main-deploy.yml)
[![.github/workflows/ci-dev.yml](https://github.com/calebjenkins/WestDiscGolf.MoqExtensions/actions/workflows/ci-dev.yml/badge.svg)](https://github.com/calebjenkins/WestDiscGolf.MoqExtensions/actions/workflows/ci-dev.yml)

Extension method for using [Moq](https://github.com/moq) with [Microsoft.Extensions.Logging](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.logging?view=dotnet-plat-ext-7.0)


Forked from https://github.com/WestDiscGolf/Random/tree/master/LoggerUnitTests

[Original Blog Post](https://www.adamstorr.co.uk/blog/mocking-ilogger-with-moq)
   |   [Package request](https://github.com/WestDiscGolf/Random/issues/2)

## Installing KeyValueRepo

You should install [MoqExtensions with NuGet](https://www.nuget.org/packages/WestDiscGolf.MoqExtensions):

    Install-Package WestDiscGolf.MoqExtensions
    
Or via the .NET Core command line interface:

    dotnet add package WestDiscGolf.MoqExtensions

Either command, from Package Manager Console or .NET Core CLI, will download and install all required dependencies.

## Contributing
- PRs should be against the `develop` branch.
- Merged PRs to `develop` will trigger a `[version]-ci-[buildnumber]` deployment to nuget, assuming all unit tests pass.
- Merged PRs to `main` will trigger a [version] deployment to nuget, assuming all of the tests pass.
- Merges to all other pranches will trigger a `CI` action to run all unit tests

## Versioning
The package `version` is defined in the `MoqExtensions.csproj` file, using .NET SDK style structure. We follow `semantic versioning` for this package.

## Usage
Use these extensions when working with `Moq` and `Microsoft.Extensions.Logging.ILogger<>` since Microsoft's implementation of the `ILogger` mostly relies on extension methods, and not on methods defined in the actual `ILogger` interface. This extension method takes a "mock around" approach - to get around the ILogger extension methods and to assert against what they are doing beneath the abstractions.

## Examples
More examples in [LoggerTest.cs](https://github.com/calebjenkins/WestDiscGolf.MoqExtensions/blob/main/src/MoqExtensionsTests/LoggerTest.cs)
```csharp
    [Fact]
    public void VerifyWasCalledWithReusableExtension()
    {
        // Arrange
        var loggerMock = new Mock<ILogger<PleaseTestMe>>();
        var sut = new PleaseTestMe(loggerMock.Object);

        // Act
        sut.RunMe();

        // Assert
        loggerMock.VerifyDebugWasCalled();
    }
```

```csharp
    [Fact]
    public void VerifyWasCalledWithReusableExtensionWithMessage()
    {
        // Arrange
        var loggerMock = new Mock<ILogger<PleaseTestMe>>();
        var sut = new PleaseTestMe(loggerMock.Object);

        // Act
        sut.RunMe();

        // Assert
        loggerMock.VerifyDebugWasCalled("Logging this ...");
    }
```

```csharp
    [Fact]
    public void VerifyLoopTest_2()
    {
        // Arrange
        var loggerMock = new Mock<ILogger<PleaseTestMe>>();
        var sut = new PleaseTestMe(loggerMock.Object);

        // Act
        sut.RunMeLoop();

        // Assert
        loggerMock.VerifyLogging("Logging Multiple Times ...", LogLevel.Debug, Times.Exactly(3));
    }
```

More examples in [LoggerTest.cs](https://github.com/calebjenkins/WestDiscGolf.MoqExtensions/blob/main/src/MoqExtensionsTests/LoggerTest.cs)

## Change Log
- 1.0.2 - readme and links updated to correct blog page
- 1.0.1 - added .NET 7
- 1.0.0 - ininitial release