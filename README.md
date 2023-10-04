# build.publish.mps

[![artifacts.itemis.cloud](https://img.shields.io/badge/dynamic/xml?url=https://artifacts.itemis.cloud/repository/maven-mps/com/jetbrains/mps/maven-metadata.xml&label=artifacts.itemis.cloud&color=success&query=.//versioning/latest)](https://artifacts.itemis.cloud/#browse/browse:maven-mps:com%2Fjetbrains)
[![Github pages](https://img.shields.io/badge/Github-pages-success)](https://github.com/orgs/mbeddr/packages?repo_name=build.publish.mps)

This repository contains a gradle script for publishing MPS and its jars to a few Maven repositories. You can use these dependencies, for example, in a Gradle or maven build script.

Example usage: [model checker of mps-gradle-plugin](https://github.com/mbeddr/mps-gradle-plugin/blob/0da7e4ba4d5ef07504c42d0b77ab097054f02ee8/modelcheck/build.gradle.kts#L41)

The script for older MPS versions can be found in the mps/**X** branches where **X** is a major MPS version.

The following artifacts are published:

**As a zip file**:

- com.jetbrains.mps: if a jar file is not published, you can still extract it from this full zip file.

**As a jar file**:

- *com.jetbrains.mps-core*
- *com.jetbrains.mps-editor*
- *com.jetbrains.mps-editor-api*
- *com.jetbrains.mps-editor-runtime*
- *com.jetbrains.mps-openapi*
- *com.jetbrains.mps-tool*
- *com.jetbrains.mps-run*
- *com.jetbrains.mps-environment*
- *com.jetbrains.mps-platform*
- *com.jetbrains.util*
- *com.jetbrains.mps-console-ide-commands-runtime*
- *com.jetbrains.mps-messaging*
- *com.jetbrains.mps-modelchecker*
- *com.jetbrains.mps-httpsupport-runtime*
- *com.jetbrains.mps-project-check*
- *com.jetbrains.mps-workbench*
- *com.jetbrains.annotations*

**Notes**:
- Since 2021.1, the artifact *com.jetbrains.platform-concurrency* is no longer available.
- Since 2022.2, the artifact *com.jetbrains.platform-api* is no longer available.


# Adding a dependency on arbitrary JAR files from an MPS distribution

This repository only publishes some JAR files and does not publish additional JARs retroactively for older versions. If you are using Gradle, you can add a dependency on an arbitrary selection of JARs from within the MPS distribution as follows:

```kotlin
val mpsRuntime by configurations.creating
val mpsZip by configurations.creating

dependencies {
    mpsZip("com.jetbrains:mps:...")
    mpsRuntime(zipTree({ mpsZip.singleFile }).matching {
        include("lib/mps-core.jar")
        include("lib/mps-environment.jar")
        include("lib/mps-platform.jar")
        include("lib/mps-openapi.jar")
        include("lib/mps-logging.jar")
        include("lib/platform-api.jar")
        include("lib/util.jar")
    })
}
```
