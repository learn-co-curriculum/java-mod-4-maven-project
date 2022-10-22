# Creating a Maven Project

## Learning Goals

- Create a Maven-based Java project in IntelliJ
- Define the structure of a Maven project
- Define the parts of a pom.xml configuration file

## Introduction

IntelliJ supports 3 build systems: IntelliJ's
native build system, Maven, and Gradle.
The native build system works well to build basic Java projects.
When a project requires custom plugins or tasks,  Gradle or Maven may be a
better choice.

We will step through the process of using IntelliJ to create a Java project
that will be built using Maven. 

Maven comes bundled with IntelliJ, so we don't have
to install anything to get started.

## Create a Maven project
  
Open IntelliJ then select "File/New/Project" from the menu-bar
or click the "New Project" button.
    
![new maven project](https://curriculum-content.s3.amazonaws.com/6002/creating-a-maven-project/newproject.png)

1. Enter "example-app" for the project name.
2. Enter a folder location to store the project.
3. Select "Java" as the language.
4. Select "Maven" as the build system.
5. Select a Java version that is at least Java 11.
6. Check  "Add sample code"
7. Enter "org.example" for the GroupId.
8. Enter "example-app" for the ArtifactId.
9. Press "Create".

IntelliJ creates the new project with the sample `Main` class.
   
![new project view](https://curriculum-content.s3.amazonaws.com/6002/creating-a-maven-project/projectfolders.png)

Press the green run button to execute the `main` method.
The `target` folder is created after the code compiles and runs.
If the folder is not visible in the project view,
click the settings icon then select
"Tree Appearance/Show Excluded Files".

![show excluded files](https://curriculum-content.s3.amazonaws.com/6002/creating-a-maven-project/excludedfiles.png)


## Maven Directory Structure

A Maven project has a
[standard directory structure](https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html)
for source code and configurations. We’ll only look at the minimal structure in
this lesson to get started.

The following is a basic structure of a Maven project:

```text
└── /example-app
		├── src
		│   ├── main
		│   │   ├── java
		│   │   └── resources
		│   └── test
		│       ├── java
		│       └── resources
		├── target
		└── pom.xml
```

- `src/main/java`: this is where the application source files are stored.
- `src/main/resources`: the .properties files, xml config, certificates, and
  other config files are stored here.
- `src/test/java`: the source code for tests are stored here.
- `src/test/resources`: this is where test config files are stored.
- `/target`: this stores the output files of the build process.
- `pom.xml`: The POM (Project Object Model) describes the libraries and plugins needed, which Java version to build, and more.

There are additional directories that you may see in a standard directory. Check out
[the official documentation](https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html)
for a list of these directories.

IntelliJ adds additional directories to the project as well.

## pom.xml

Open the `pom.xml` file to explore its contents:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>example-app</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

</project>
```

We’ll start examining the pom file from the line where
`<groupId>org.example</groupId>` starts. Everything before that contains the XML
namespaces and the XML model version which we won't need to modify. We’ll look
at the sections below that and discuss them.

### Coordinates

Since all projects need to be unique Maven provides a standard way to
distinguish between projects using
[coordinates](https://maven.apache.org/pom.html#maven-coordinates).

```xml
<groupId>org.example</groupId>
<artifactId>example-app</artifactId>
<version>1.0-SNAPSHOT</version>
```

1. **groupId:** This is usually the group, company, or department creating the
   project. We generally use the domain name in reverse order. In this case, the
   company domain is `[example.org](http://example.org)` so we’ve written it as
   `org.example` in the POM file.
2. **artifactId:** A unique name for the project under the groupId. For example,
   if the company is creating multiple libraries, each library would have a
   unique artifactId but the same groupId.
3. **version:** This indicates the current version of the project. Each new
   release would get a new version. You can check out what a SNAPSHOT version
   means
   [here](https://maven.apache.org/guides/getting-started/index.html#what-is-a-snapshot-version).

![Maven coordinates](https://curriculum-content.s3.amazonaws.com/6002/creating-a-maven-project/coordinates.png)

In this diagram, the top level represents the groupId, the middle level
represents artifactId, and finally the bottom level represents the version.
Our current project contains the example-app artifact, but other projects
could contain the helper-library and admin-app.

### Properties

The properties section specifies values that can be used anywhere within a POM
or as default values by plugins.

```xml
<properties>
   <maven.compiler.source>11</maven.compiler.source>
   <maven.compiler.target>11</maven.compiler.target>
   <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

The `<maven.compiler.source>11</maven.compiler.source>` tag specifies the
minimum Java version required for the project and the
`<maven.compiler.target>11</maven.compiler.target>` tag specifies what version
the project is expected to run on.

The `<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>`
specifies the encoding for resources like .properties and text files. Maven will
use the operating system’s default encoding if it’s not specified which could
lead to incompatibility across systems.

There are many other optional elements that can be added to pom.xml.  Maven
requires the project, modelVersion, groupId, artifactId, and version elements
as a bare minimum.

## Conclusion

We’ve learned how to create a Maven project and learned the basic properties of
the POM file.

## Resources

- [Maven download](https://maven.apache.org/download.cgi)   
- [Maven standard directory structure](https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html)   
- [Maven coordinates](https://maven.apache.org/pom.html#maven-coordinates)   
- [Maven pom](https://maven.apache.org/pom.html)    
