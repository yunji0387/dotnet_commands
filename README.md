# .NET Commands

## [Learning Source](https://learn.microsoft.com/en-us/training/dotnet/)

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

## File system in .NET
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

[useful resource](https://learn.microsoft.com/en-us/training/modules/dotnet-files/1-introduction)

### Searching method
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
#### List files in a specific directory
```c#
IEnumerable<string> files = Directory.EnumerateFiles("stores");

foreach (var file in files)
{
    Console.WriteLine(file);
}
```

#### List all content in a directory and all subdirectories
```c#
// Find all *.txt files in the stores folder and its subfolders
IEnumerable<string> allFilesInAllFolders = Directory.EnumerateFiles("stores", "*.txt", SearchOption.AllDirectories);

foreach (var file in allFilesInAllFolders)
{
    Console.WriteLine(file);
}
```

#### Determine the current directory
```c#
Console.WriteLine(Directory.GetCurrentDirectory());
```

#### Work with special directories
```c#
string docPath = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);
```

#### Special path characters
To help you use the correct  Directory Separator in different operating systems(ex. macOs, Windows)
```c#
Console.WriteLine($"stores{Path.DirectorySeparatorChar}201");
// returns:
// stores\201 on Windows
//
// stores/201 on macOS
```

#### Join paths
```c#
Console.WriteLine(Path.Combine("stores","201")); // outputs: stores/201
```

#### Determine filename extensions
```c#
Console.WriteLine(Path.GetExtension("sales.json")); // outputs: .json
```

#### Get everything you need to know about a file or path
```c#
string fileName = $"stores{Path.DirectorySeparatorChar}201{Path.DirectorySeparatorChar}sales{Path.DirectorySeparatorChar}sales.json";

FileInfo info = new FileInfo(fileName);

Console.WriteLine($"Full Name: {info.FullName}{Environment.NewLine}Directory: {info.Directory}{Environment.NewLine}Extension: {info.Extension}{Environment.NewLine}Create Date: {info.CreationTime}"); // And many more
```

<!-- /MarkdownTOC -->
</details>



<!-- /MarkdownTOC -->
</details>

