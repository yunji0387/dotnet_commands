# .NET Commands

### Prerequisite
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

- [C# commands](https://github.com/yunji0387/CSharp_commands)
- [(video tutorials) .NET 101](https://learn.microsoft.com/en-us/shows/NET-Core-101/?WT.mc_id=Educationaldotnet-c9-scottha)
- [(video tutorials) ASP.NET Core 101](https://learn.microsoft.com/en-us/shows/ASPNET-Core-101/?WT.mc_id=Educationaspnet-c9-niner)
- [(video tutorials) ASP.NET Core Web API 101](https://learn.microsoft.com/en-us/shows/Beginners-Series-to-Web-APIs/)

<!-- /MarkdownTOC -->
</details>

## Learning Source
- [.NET Learn](https://learn.microsoft.com/en-us/training/dotnet/)

## Table of Contents
1. [Set up development environment](#setup)
2. [How to create, build & run .NET project](#create_dotnet)
3. [How to create, build & run c#](#create_csharp)
4. [How to install/uninstall/restore/check a package/dependency](#dotnet_dependency)
5. [How to debug .NET code in VS Code](#dotnet_debug)
6. [File system in .NET](#dotnet_filesystem)
7. [Web API with ASP.NET Core controllers](#web_api_asp_dotnet)

<a id="setup"></a>
## Set up development environment
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

1. Download and install [Visual Studio 2022](https://visualstudio.microsoft.com/vs/)
   - In the visual studio workloads, install the following:
     - ...
2. Download and install both [.NET SDK](https://dotnet.microsoft.com/en-us/download) and [Visual Studio Code](https://code.visualstudio.com/).

<!-- /MarkdownTOC -->
</details>

<a id="create_dotnet"></a>
## How to create, build & run .NET project
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

1. create c# project
   - in Terminal run:
   ```c#
   dotnet new console -f net6.0
   ```
   - This command creates a Program.cs file in your folder with a basic "Hello World" program already written, along with a C# project file named DotNetDependencies.csproj. You should now have access to these files.
     ```bash
     -| obj
     -| DotNetDependencies.csproj
     -| Program.cs
     ```
3. In terminal, run:
   ```bash
   dotnet run
   ```

<!-- /MarkdownTOC -->
</details>

<a id="create_csharp"></a>
## How to create, build & run c#
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

1. make sure to have .NET SDK install
   - visit this [link for more detail](https://learn.microsoft.com/en-us/training/modules/install-configure-visual-studio-code/6-exercise-install-dotnet).
2. make sure to have c# extension install in vs code
   - visit this [link for more detail](https://learn.microsoft.com/en-us/training/modules/install-configure-visual-studio-code/5-exercise-configure-visual-studio-code).
3. create c# project
   - in Terminal run:
   ```c#
   dotnet new console -o ./CsharpProjects/TestProject
   ```
4. build c# project
   - first make sure terminal path located in the project folder, then run:
   ```c#
   dotnet build
   ```
5. run c# project
   - first make sure terminal path located in the project folder and has done step 4, then run:
   ```c#
   dotnet run
   ```

<!-- /MarkdownTOC -->
</details>

<a id="dotnet_dependency"></a>
## How to install/uninstall/restore/check a package/dependency
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

```bash
dotnet add package <dependency name>
```

- To check your installed package list
  ```bash
  dotnet list package
  ```
  ```bash
  dotnet list package --include-transitive
  ```

- To restore (when you create or clone a project)
  ```bash
  dotnet restore
  ```
- To delete
  ```bash
  dotnet remove package <name of dependency>
  ```
- Find and update outdated packages
  ```bash
  dotnet list package --outdated
  ```
  ```bash
  dotnet add package <package name>
  ```

<!-- /MarkdownTOC -->
</details>

<a id="dotnet_debug"></a>
## How to debug .NET code in VS Code
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

- [Useful tutorial](https://learn.microsoft.com/en-us/training/modules/dotnet-debug/3-analyze-your-program-state)
- Remeber to change console setting in launch.json from "internalConsole" to "integratedTerminal" when you want debug console to handle terminal input.

### Debug - write information to output windows
[Useful source 1](https://learn.microsoft.com/en-us/training/modules/dotnet-debug/5-logging-and-tracing),
[Useful source 2](https://learn.microsoft.com/en-us/training/modules/dotnet-debug/6-use-logging-and-tracing)
1. import Debug methods library
   ```c#
   using System.Diagnostis;
   ```
2. example:
   ```c#
   using System.Diagnostics;
   
   int result = Fibonacci(5);
   Console.WriteLine(result);
   
   static int Fibonacci(int n)
   {
       Debug.WriteLine($"Entering {nameof(Fibonacci)} method");
       Debug.WriteLine($"We are looking for the {n}th number");
       int n1 = 0;
       int n2 = 1;
       int sum;
   
       for(int i=2; i<=n ; i++)
       {
           sum = n1 + n2;
           n1 = n2;
           n2 = sum;
           Debug.WriteLineIf(sum == 1, $"sum is 1, n1 is {n1}, n2 is {n2}");
       }
       return n == 0 ? n1 : n2;
   }

   ```
### Debug - check for conditions with Assert
[Useful source](https://learn.microsoft.com/en-us/training/modules/dotnet-debug/6-use-logging-and-tracing)

Example: 
```cs
using System.Diagnostics;

// See https://aka.ms/new-console-template for more information

int result = Fibonacci(6);

static int Fibonacci(int n)
{
    int n1 = 0;
    int n2 = 1;
    int sum;

    for (int i = 2; i <= n; i++)
    {
        sum = n1 + n2;
        n1 = n2;
        n2 = sum;
    }
    // If n2 is 5 continue, else break.
    Debug.Assert(n2 == 5, "The return value is not 5 and it should be.");
    return n == 0 ? n1 : n2;
}
```
1. Run with debugging mode
   You should see below message in your debug console:
   ```output
   ---- DEBUG ASSERTION FAILED ----
   ---- Assert Short Message ----
   The return value is not 5 and it should be.
   ---- Assert Long Message ----
   
      at Program.<<Main>$>g__Fibonacci|0_0(Int32 n) in C:\Users\Jon\Desktop\DotNetDebugging\Program.cs:line 23
      at Program.<Main>$(String[] args) in C:\Users\Jon\Desktop\DotNetDebugging\Program.cs:line 3
   ```
2. Run with terminal "dotnet run"
   You should see below message in your terminal:
   ```output
   Process terminated. Assertion failed.
   The return value is not 5 and it should be.
      at Program.<<Main>$>g__Fibonacci|0_0(Int32 n) in C:\Users\Jon\Desktop\DotNetDebugging\Program.cs:line 23
      at Program.<Main>$(String[] args) in C:\Users\Jon\Desktop\DotNetDebugging\Program.cs:line 3
   ```
   - To run without Assertion with terminal, use:
     ```bash
     dotnet run --configuration Release
     ```

<!-- /MarkdownTOC -->
</details>

<a id="dotnet_filesystem"></a>
## File system in .NET
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

[useful resource](https://learn.microsoft.com/en-us/training/modules/dotnet-files/1-introduction)

### Searching methods
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

#### List all directories
```c#
IEnumerable<string> listOfDirectories = Directory.EnumerateDirectories("stores");

foreach (var dir in listOfDirectories) {
    Console.WriteLine(dir);
}
```
---

#### List files in a specific directory
```c#
IEnumerable<string> files = Directory.EnumerateFiles("stores");

foreach (var file in files)
{
    Console.WriteLine(file);
}
```
---

#### List all content in a directory and all subdirectories
```c#
// Find all *.txt files in the stores folder and its subfolders
IEnumerable<string> allFilesInAllFolders = Directory.EnumerateFiles("stores", "*.txt", SearchOption.AllDirectories);

foreach (var file in allFilesInAllFolders)
{
    Console.WriteLine(file);
}
```
---

#### Determine the current directory
```c#
Console.WriteLine(Directory.GetCurrentDirectory());
```
---

#### Work with special directories
```c#
string docPath = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);
```
---

#### Special path characters
To help you use the correct  Directory Separator in different operating systems(ex. macOs, Windows)
```c#
Console.WriteLine($"stores{Path.DirectorySeparatorChar}201");
// returns:
// stores\201 on Windows
//
// stores/201 on macOS
```
---

#### Join paths
```c#
Console.WriteLine(Path.Combine("stores","201")); // outputs: stores/201
```
---

#### Determine filename extensions
```c#
Console.WriteLine(Path.GetExtension("sales.json")); // outputs: .json
```
---

#### Get everything you need to know about a file or path
```c#
string fileName = $"stores{Path.DirectorySeparatorChar}201{Path.DirectorySeparatorChar}sales{Path.DirectorySeparatorChar}sales.json";

FileInfo info = new FileInfo(fileName);

Console.WriteLine($"Full Name: {info.FullName}{Environment.NewLine}Directory: {info.Directory}{Environment.NewLine}Extension: {info.Extension}{Environment.NewLine}Create Date: {info.CreationTime}"); // And many more
```
---

<!-- /MarkdownTOC -->
</details>

### create methods
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

#### Create directories
```c#
Directory.CreateDirectory(Path.Combine(Directory.GetCurrentDirectory(), "stores","201","newDir"));
```
---

#### Make sure directories exist
```c#
bool doesDirectoryExist = Directory.Exists(filePath);
```
---

#### Create files
```c#
File.WriteAllText(Path.Combine(Directory.GetCurrentDirectory(), "greeting.txt"), "Hello World!");
```
---

<!-- /MarkdownTOC -->
</details>

### Read and write to files methods
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

#### Read data from files
```c#
File.ReadAllText($"stores{Path.DirectorySeparatorChar}201{Path.DirectorySeparatorChar}sales.json");
```
The return object from ReadAllText is a string.
```json
{
  "total": 22385.32
}
```
---
#### Parse data in files
In bash, add "json.NET" package
```bash
dotnet add package Newtonsoft.Json
```
Then, add using Newtonsoft.Json to the top of your class file:
```c#
using Newtonsoft.Json; 
```
And use the JsonConvert.DeserializeObject method:
```c#
var salesJson = File.ReadAllText($"stores{Path.DirectorySeparatorChar}201{Path.DirectorySeparatorChar}sales.json");
var salesData = JsonConvert.DeserializeObject<SalesTotal>(salesJson);

Console.WriteLine(salesData.Total);

class SalesTotal
{
  public double Total { get; set; }
}
```
---
#### Write data to files
```c#
var data = JsonConvert.DeserializeObject<SalesTotal>(salesJson);

File.WriteAllText($"salesTotalDir{Path.DirectorySeparatorChar}totals.txt", data.Total.ToString());

// totals.txt
// 22385.32
```
---
#### Append data to files
```c#
var data = JsonConvert.DeserializeObject<SalesTotal>(salesJson);

File.AppendAllText($"salesTotalDir{Path.DirectorySeparatorChar}totals.txt", $"{data.Total}{Environment.NewLine}");

// totals.txt
// 22385.32
// 22385.32
```
---

<!-- /MarkdownTOC -->
</details>

<!-- /MarkdownTOC -->
</details>

<a id="web_api_asp_dotnet"></a>
## Web API with ASP.NET Core controllers
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->



<!-- /MarkdownTOC -->
</details>


<a id="title"></a>
## title
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->



<!-- /MarkdownTOC -->
</details>


