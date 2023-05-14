 MoqExtensions
[![.github/workflows/ci.yml](https://github.com/calebjenkins/WestDiscGolf.MoqExtensions/actions/workflows/ci.yml/badge.svg)](https://github.com/calebjenkins/WestDiscGolf.MoqExtensions/actions/workflows/ci.yml)

Extension method for using Moq with Microsoft.Extensions.Logger


Forked from https://github.com/WestDiscGolf/Random/tree/master/LoggerUnitTests

[Original Blog Post](https://adamstorr.azurewebsites.net/blog/mocking-ilogger-with-moq)
   |   [Tracking package request](https://github.com/WestDiscGolf/Random/issues/2)

## Installing KeyValueRepo

You should install [Extensions with NuGet](https://www.nuget.org/packages/Calebs.KeyValueRepo):

    Install-Package **Coming.Soon **
    
Or via the .NET Core command line interface:

    dotnet add package **Coming.Soon**

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