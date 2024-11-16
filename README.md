# 15112024A
simple class that generates color text in console

## help

`dotnet --help`

## create

`dotnet new list`\
`dotnet new classlib`

## build

`dotnet build`

## pack tu NuGet Package

`dotnet pack -c Release -o out`


## Details

# Creating the NuGet Package
1. Add Package Metadata: Open the .csproj file of your ColorLibrary and add the necessary package metadata. Here’s an example:
``
<PropertyGroup>
  <TargetFramework>net6.0</TargetFramework>
  <PackageId>ColorLibrary</PackageId>
  <Version>1.0.0</Version>
  <Authors>YourName</Authors>
  <Company>YourCompany</Company>
  <Description>A library for colour strings</Description>
  <PackageTags>color;library</PackageTags>
</PropertyGroup>
``
2. Pack the Library: Use the dotnet pack command to create a NuGet package from your class library. This command will generate a .nupkg file in the bin\Debug or bin\Release directory, depending on your build configuration.

`dotnet pack -c Release`
3. Publish the Package: To publish your package to NuGet.org or another NuGet feed, use the dotnet nuget push command. You will need an API key from the NuGet feed you are publishing to.

`dotnet nuget push bin/Release/ColorLibrary.1.0.0.nupkg -k YourApiKey -s https://api.nuget.org/v3/index.json`

# Using the NuGet Package in ColorApp
1. Add the NuGet Package: In your ColorApp project, add a reference to the ColorLibrary NuGet package. You can do this using the dotnet add package command:

`dotnet add package ColorLibrary --version 1.0.0`
2. Update Program.cs: Modify your Program.cs file to use the ColorLibrary. Here’s an example:

``
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
``
3. Build and Run Your Application: Build your application using the following command:

`dotnet build`\

Then, run your application:

`dotnet run --project ColorApp`

## references
[web-commandline](https://learn.microsoft.com/en-us/dotnet/standard/commandline/)\
[git-commandline](https://github.com/dotnet/docs/blob/main/docs/standard/commandline/get-started-tutorial.md)
