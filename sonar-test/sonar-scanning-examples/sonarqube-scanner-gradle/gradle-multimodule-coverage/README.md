# SonarQube-Scanner-Gradle Multi-Module Code Coverage

(Originally from https://github.com/SonarSource/sonar-scanning-examples)

This example project demonstrates how to analyze a multimodule project with Jacoco code coverage built with Gradle.

## Prerequisites
* [SonarQube](http://www.sonarqube.org/downloads/) 7.9+
* A Gradle wrapper is included that bundles Gradle. All other required plugins will be pulled by Gradle as needed.

## Usage
Run the following command (update `sonar.host.url`, `sonar.login`, `sonar.password`, etc. properties as needed either at command line or in `sonar.gradle`):
* On Unix-like systems:
  ` ./gradlew clean build codeCoverageReport -Dsonar.host.url=http://localhost:9000 -Dsonar.login=admin -Dsonar.password=admin sonarqube`
* On Windows:
  `.\gradlew.bat clean build codeCoverageReport -Dsonar.host.url=http://localhost:9000 -Dsonar.login=admin -Dsonar.password=admin sonarqube`

## Coverage
This example project is based on the original example project from Gradle's [sample project](https://docs.gradle.org/6.4-rc-1/samples/sample_jvm_multi_project_with_code_coverage.html) for reporting code coverage for Jacoco (Gradle 6.4-rc-1 and Gradle 6.6.1) as well as Andranik Azizbekian's [article](https://developer.disqo.com/blog/setup-android-project/)  integrating SonarQube with a Kotlin Android project.

Here are the important changes compared to the original Gradle sample project linked above in order for SonarQube to pick up the code coverage metric:
* ensure `settings.gradle` references your modules
* add `id org.sonarqube" version "3.2.0"` to the `plugins{}` block to root `build.gradle`  (use a different SonarScanner for Gradle version if you so desire)
* add the following to `subprojects{}` block of root `build.gradle`:
    * ```shell
      apply plugin: "org.sonarqube"
      sonarqube {
          properties {
              property "sonar.coverage.jacoco.xmlReportPaths", "$projectDir.parentFile.path/build/reports/jacoco/codeCoverageReport/codeCoverageReport.xml"
          }
      }
      ```
* add a new file to root of project called `sonar.gradle` with the following contents:
    * ```shell
      apply plugin: "org.sonarqube"
      sonarqube {
         properties {
            property 'sonar.projectName', 'gradle-multimodule'
            property "sonar.projectKey", "gradle-multimodule"
            // Add other analysis parameters here if you don't
            // want to add it to the Sonar scanner command line:
            // property "sonar.host.url", "yoursonarqubeurl"
            // property "sonar.login", "yourlogintoken"
            // etc.
        }
      }
      ```
* add `apply from: "$project.rootDir/sonar.gradle"` to root `build.gradle`


For other forms of Gradle and Maven code coverage, see [test coverage](https://community.sonarsource.com/t/coverage-test-data-importing-jacoco-coverage-report-in-xml-format) in the SonarSource community forum. There are many other guides in the [Community guides](https://community.sonarsource.com/c/announce/guides/) section to assist you as well.

## Known Issue(s)
* You may notice the `Bytecode of dependencies was not provided for analysis of source files, you might end up with less precise results. Bytecode can be provided using sonar.java.libraries property.` warning. This is primarily due to the lack of dependencies (i.e. empty `dependencies {}` block) in this example project, so it is harmless. Your actual project may include dependencies. To ensure not needing to configure `sonar.java.binaries`, ensure usage of Sonar Scanner for Gradle; setting of `sonar.java.binaries ` is done automatically for you.
