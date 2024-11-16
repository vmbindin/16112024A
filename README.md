# 15112024A
simple class that generates color text in console

## help

`dotnet --help`

## create

`dotnet new list`\
`dotnet new classlib`

## build

`dotnet build`

## pack to NuGet Package

`dotnet pack -c Release -o out`

## using NuGet Package

`dotnet add package <package-name> --source <path-to-local-nuget-source>`

## Details

# Create a NuGet Package method 1
1. **Add Package Metadata**: Open the .csproj file of your ColorLibrary and add the necessary package metadata. Here’s an example:
```
<PropertyGroup>
  <TargetFramework>net6.0</TargetFramework>
  <PackageId>ColorLibrary</PackageId>
  <Version>1.0.0</Version>
  <Authors>YourName</Authors>
  <Company>YourCompany</Company>
  <Description>A library for colour strings</Description>
  <PackageTags>color;library</PackageTags>
</PropertyGroup>
```
2. **Pack the Library**: Use the dotnet pack command to create a NuGet package from your class library. This command will generate a .nupkg file in the bin\Debug or bin\Release directory, depending on your build configuration.

`dotnet pack -c Release`

3. **Publish the Package**: To publish your package to NuGet.org or another NuGet feed, use the dotnet nuget push command. You will need an API key from the NuGet feed you are publishing to.

`dotnet nuget push bin/Release/ColorLibrary.1.0.0.nupkg -k YourApiKey -s https://api.nuget.org/v3/index.json`

# Using the NuGet Package in ColorApp
1. **Add the NuGet Package**: In your ColorApp project, add a reference to the ColorLibrary NuGet package. You can do this using the dotnet add package command:

`dotnet add package ColorLibrary --version 1.0.0`

2. **Update Program.cs**: Modify your Program.cs file to use the ColorLibrary. Here’s an example:

```
using System;
using ColorLibrary;

namespace ColorApp
{
    class Program
    {
        static void Main(string[] args)
        {
            Colors colors = new Colors();
            Console.WriteLine(colors.GetRed());
            Console.WriteLine(colors.GetGreen());
            Console.WriteLine(colors.GetBlue());
            Console.WriteLine(colors.GetYellow());
        }
    }
}
```
3. **Build and Run Your Application**: Build your application using the following command:

`dotnet build`

Then, run your application:

`dotnet run --project ColorApp`

# Create a NuGet Package method 2

If you want to use a NuGet package without publishing it to NuGet.org, you can create and use a local NuGet package source. Here’s how you can do it:

1. **Create the NuGet Package**: First, create your NuGet package using the dotnet pack command:

`dotnet pack -c Release`\
This command will generate a .nupkg file in the bin\Release directory.

2. **Create a Local NuGet Source**: Create a folder on your local machine to act as your local NuGet source. For example, you can create a folder named LocalNuGetPackages.

3. **Copy the NuGet Package**: Copy the .nupkg file to the LocalNuGetPackages folder.

4. **Add the Local Source to NuGet Config**: Open Visual Studio and go to Tools > Options > NuGet Package Manager > Package Sources. Click the + button to add a new package source, and set the name and path to your LocalNuGetPackages folder. Click OK to save the changes.

5. **Reference the Local NuGet Package**: In your project, you can now reference the local NuGet package. Open the Package Manager Console and run the following command:

`dotnet add package ColorLibrary --source <path-to-LocalNuGetPackages>`\
Replace <path-to-LocalNuGetPackages> with the actual path to your local NuGet source folder.

6. **Use the Package in Your Project**: Now you can use the ColorLibrary in your project just like any other NuGet package. Here’s an example of how to use it in your Program.cs file:
```
using System;
using ColorLibrary;

namespace ColorApp
{
    class Program
    {
        static void Main(string[] args)
        {
            Colors colors = new Colors();
            Console.WriteLine(colors.GetRed());
            Console.WriteLine(colors.GetGreen());
            Console.WriteLine(colors.GetBlue());
            Console.WriteLine(colors.GetYellow());
        }
    }
}
```
By following these steps, you can create and use a local NuGet package without publishing it to NuGet.org.

# Add NuGet source

## How to use the dotnet add package command with the --source option to add a package from a local NuGet source:

1. **Create a Local NuGet Source**: First, create a folder to act as your local NuGet source. For example, you can create a folder named LocalNuGetPackages.

2. **Copy the NuGet Package**: Copy your .nupkg file to the LocalNuGetPackages folder.

3. **Add the Local Source to NuGet Config**: Open a terminal and run the following command to add your local NuGet source:

`dotnet nuget add source <path-to-LocalNuGetPackages> -n LocalNuGetSource`\
Replace <path-to-LocalNuGetPackages> with the actual path to your local NuGet source folder.

4. **Add the Package to Your Project**: Navigate to your project directory and run the following command to add the package from your local source:

`dotnet add package ColorLibrary --source <path-to-LocalNuGetPackages>`\
Replace <path-to-LocalNuGetPackages> with the actual path to your local NuGet source folder.

## Here’s a concrete example:

1. **Create a Local NuGet Source**: Create a folder named LocalNuGetPackages at C:\LocalNuGetPackages.

2. **Copy the NuGet Package**: Copy ColorLibrary.1.0.0.nupkg to C:\LocalNuGetPackages.

3 **Add the Local Source to NuGet Config**:

`dotnet nuget add source C:\LocalNuGetPackages -n LocalNuGetSource`\
Add the Package to Your Project: Navigate to your project directory and run:

`dotnet add package ColorLibrary --source C:\LocalNuGetPackages`\
This will add the ColorLibrary package from your local NuGet source to your project.

## Issues

It sounds like you're encountering an issue where the dotnet add package command is unable to find a version of the package you're trying to add. This can happen for a few reasons, and here are some steps you can take to troubleshoot and resolve the issue:

1. **Check the Package Source**: Ensure that the package source is correctly configured and accessible. You can list the configured package sources using the following command:

`dotnet nuget list source`\
If the source is missing or incorrect, you can add or update it using:

`dotnet nuget add source <source-url> -n <source-name>`\
2. **Specify the Version**: If the package version is not specified, dotnet might not be able to find the correct version. You can specify the version explicitly using the --version option:

`dotnet add package <package-name> --version <version-number>`\
Check for Typos: Ensure that the package name and version are spelled correctly. Even a small typo can cause the command to fail.

3. **Clear NuGet Cache**: Sometimes, clearing the NuGet cache can resolve issues with package resolution. You can clear the cache using:

`dotnet nuget locals all --clear`\
Check Network Connectivity: Ensure that your network connection is stable and that there are no firewall or proxy issues blocking access to the NuGet source.

4. **Use a Local NuGet Source**: If you have a local NuGet package, you can add it to your project by specifying the local source:

`dotnet add package <package-name> --source <path-to-local-nuget-source>`

## references
[web-commandline](https://learn.microsoft.com/en-us/dotnet/standard/commandline/)\
[git-commandline](https://github.com/dotnet/docs/blob/main/docs/standard/commandline/get-started-tutorial.md)
