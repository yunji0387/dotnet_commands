# Blazor command

## Learning Source
- [.NET Learn](https://learn.microsoft.com/en-us/training/dotnet/)

## Table of Contents
1. [How to create & run Blazor app](#how_to_create)

<a id="how_to_create"></a>
## How to create & run Blazor app with Visual Studio
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

### How to create
1. Create a new folder named <app name>
2. open the folder in Terminal, and run:
   ```bash
   dotnet new blazorserver -f net6.0
   ```
   This command creates a basic Blazor server project with all required files and pages, along with a C# project file named BlazorApp.csproj.
3. If Visual Studio Code prompts you to install required assets, select Yes.

### How to run
4. In the terminal window, run:
   ```bash
   dotnet watch run
   ```

<!-- /MarkdownTOC -->
</details>
