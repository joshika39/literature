### Introduction
C# is nice and all, but as you might know it's missing some useful functionalities which could potentially help beginner or intermediate C# programmers in their way of programming.
### Motivation
When I was a first year student in my Computer Science bachelors degree, I came across a subject where `TextFileReader.dll` was given to us which was built a Prof at the Uni. What should I say.. It was full of flaws, it broke a few [OOP](https://en.wikipedia.org/wiki/Object-oriented_programming) principles. And then I realized, that C# is missing quite a few really useful services, which I then implemented in this project. My motive behind this project was to help the fellow C# developers to have an extensive but scalable toolset in their hand.

The project is open-source and it is on GitHub: [joshika39/cs-tools: Extended base C# functionalities (github.com)](https://github.com/joshika39/cs-tools)
### Composition
The project is published as a [NuGet package](https://www.nuget.org/packages/joshika39.Core) and it is using Microsoft's [`IServiceProvider`](https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection-guidelines) and a provided [`ServiceCollection`](https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection-guidelines) to register all of its default and required components. You can read about it in more details here: [Using the package · Wiki](https://github.com/joshika39/cs-tools/wiki/Using-the-package)

Most of the things can be configured in the `IApplicationSettings` which stores the following properties:
```cs
public interface IApplicationSettings  
{  
    string ApplicationConfigurationFile { get; }  
    string ConfigurationFolder { get; }  
    string? RepositoryPath { get; }  
}
```

> **NOTE**: The file is located under the /"*userhome*"/joshika40/*modulename*/

#### Repository
One of the useful tools are the `IRepository` which is basically a [repository pattern]() interface, which has a default `AJsonRepository` implementation registered in the `IServiceProvider`.

It can be used the following way for example:
```cs
// A factory is required to create the repository.
var repositoryFactory = provider.GetRequiredService<IRepositoryFactory>();

// Create the user repository in hte file: `users.json` in the repository path.
using var repository = repositoryFactory.CreateRepository<User>("users");  

// This line will make sure that the repository is instantiated.
await repository.SaveChangesAsync();  
```
#### Timer
The other quite useful par is the `IStopwatch` which has a lot of functionalities:
- It can:
	- Stop the current thread for `x` seconds
	- Wait asynchronously then notify it's listeners
	- Start periodic notification for it's subscribed listeners

### Conclusion
This package is still in development, so it's still missing some crucial documentation, but my goal will be to improve this package to help other people into the love of OOP programming.
## Contribution

Any contributions or ideas are welcome, you can open an [Enhancement Issue](https://github.com/joshika39/cs-tools/issues/new?assignees=&labels=enhancement&projects=&template=enhancement.md&title=New+Enhancement+name) or make a contribute if you have any idea. If you drop a star, I would really appreciate it!
Joshua

