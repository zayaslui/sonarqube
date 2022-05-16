# Sonarqube-Scanner for Multi-Module Java Gradle Project

This example demonstrates how to analyze a multi-module Java project with Gradle.

## Prerequisites

* [SonarQube](http://www.sonarqube.org/downloads/) 7.9+
* A gradle wrapper is included that bundles gradle. All other required plugins will be pulled by gradle as needed.

## Usage

Run the following command (updating the sonar.host.url property as appropriate):

* On Unix-like systems:

```shell
  ./gradlew -Dsonar.host.url=http://myhost:9000 sonarqube
```

* On Windows:

```powershell
  .\gradle.bat -Dsonar.host.url=http://myhost:9000 sonarqube
```
