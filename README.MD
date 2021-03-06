# BeaconHunter

Behaviour based monitoring and hunting tool built in C# tool leveraging ETW tracing. Blue teamers can use this tool to detect and respond to potential Cobalt Strike beacons. Red teamers can use this tool to discover new processes that behave like beacons to improve their opsec.

***Author***: Andrew Oliveau (@AndrewOliveau)

![alt text](https://github.com/aholdeno/BeaconHunter/blob/main/screenshots/beacon_network_score.PNG)

### TL;DR
Beacon implants injected in a benign process live in a thread with a `Wait:DelayExecution` state (probably related to Cobalt Strike's `sleep`). Find all processes that contain a thread in a `Wait:DelayExecution` state. Then, leverage ETW tracing to specifically monitor suspicious thread activity:

  - HTTPS callback frequency
  - DNS queries
  - File system (`cd`,`ls`,`upload`,`rm`)
  - Process termination (`kill`)
  - Shell commands (`run`,`execute`)

Score suspicious behavior. Log, display, and take action against them.
  
## Building / Installation

#### Pre-compiled 
<a href="https://github.com/aholdeno/BeaconHunter/releases">Release</a>

or `git clone` and go to `Release` folder.

#### .NET Framework version 

`4.5`

#### Nuggets:

Tools -> NuGet Package Manager -> Package Manager Console

* `Install-Package ConsoleTables -Version 2.4.2`
* `Install-Package Microsoft.Diagnostics.Tracing.TraceEvent -Version 2.0.64`
* `Install-Package System.Runtime.InteropServices.RuntimeInformation -Version 4.3.0`

