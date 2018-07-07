# NBomber
Very simple load testing framework for Request-response and Pub/Sub scenarios. It's 100% written in F# and targeting .NET Core and full .NET Framework.

### How to install
To install NBomber via NuGet, run this command in NuGet package manager console:
```code
PM> Install-Package VIP-Logic.NBomber
```

### Features
- [x] Request-response scenario
- [ ] Pub/Sub scenario
- [ ] Distibuted scenario (run scenario from several nodes in parallel)

### Examples
|Scenario|Examples|
|--|--|
| Request-response | [Test MongoDb with 2 READ queries and 2000 docs](https://github.com/VIP-Logic/NBomber/blob/master/samples/NBomber.Samples/Scenarios/MongoScenario.cs) |

### Supported technologies
- Supported runtimes: .NET Framework (4.6+), .NET Core (2.0+), Mono, CoreRT
- Supported languages: C#, F#, Visual Basic
- Supported OS: Windows, Linux, macOS

## Why another {x} framework for load testing?
The main reasons are:
 - **To be technology agnostic** as much as it possible (**no dependency on any protocol: HTTP, WebSockets, SSE**).
 - To be able to test .NET implementation of specific driver. During testing, it was identified many times that the performance could be slightly different because of the virtual machine(.NET, Java, PHP, Js, Erlang, different settings for GC) or just quality of drivers. For example there ware cases that drivers written in C++ and invoked from NodeJs app worked faster than drivers written in C#/.NET. Therafore it does make sense to load test your app using your concrete driver and runtime.

### What makes it very simple? 
NBomber is not really a framework but rather a foundation of building blocks which you can use to describe your test scenario, run it and get reports.
```csharp
// simple C# example
var scenario = new ScenarioBuilder(scenarioName: "Test MongoDb")                
                .AddTestFlow("READ Users", steps: new[] { mongoQuery }, concurrentCopies: 10)                
                .Build(interval: TimeSpan.FromSeconds(10));

ScenarioRunner.Run(scenario)
```
```fsharp
// simple F# example
let scenario = ScenarioBuilder(scenarioName = "Test MongoDb")                
                .AddTestFlow("READ Users", steps = [|mongoQuery|], concurrentCopies = 10)                
                .Build(interval = TimeSpan.FromSeconds(10))

ScenarioRunner.Run(scenario)
```

## Contributing
Would you like to help make NBomber even better? We keep a list of issues that are approachable for newcomers under the [good-first-issue](https://github.com/VIP-Logic/NBomber/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22) label.
