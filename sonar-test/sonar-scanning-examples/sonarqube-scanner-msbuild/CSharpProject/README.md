# SonarQube-Scanner MSBuild CSharp Project

This example demonstrates how to analyze a .NET Solution with the SonarScanner for MSBuild. Please review [cateogrization of product projects versus test projects](https://github.com/SonarSource/sonar-scanner-msbuild/wiki/Analysis-of-product-projects-vs.-test-projects) to ensure your CSharp project is scanned correctly.

## Prerequisites

* [SonarQube](http://www.sonarqube.org/downloads/) 7.9+ LTS
* [SonarScanner for .NET](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner-for-msbuild/) 4.1.0+
* [SonarSource C# Plugin](http://redirect.sonarsource.com/plugins/csharp.html) 7.15+
* [Compatible .NET Build Environment](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner-for-msbuild/)

## Usage

* Run SonarScanner for MSBuild begin phase:

```powershell
        SonarScanner.MSBuild.exe begin /k:"org.sonarqube:sonarqube-scanner-msbuild" /n:"Example of SonarScanner for MSBuild Usage" /v:"1.0"
```

* Build the project with MSBuild:

```powershell
        MSBuild.exe /t:Rebuild
```

* Run SonarScanner for MSBuild end phase:

```powershell
        SonarScanner.MSBuild.exe end
```
