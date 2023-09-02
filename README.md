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


