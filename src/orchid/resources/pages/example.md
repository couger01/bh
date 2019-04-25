Making a site with Orchid is fairly straight-forward.
This repo contains the building-blocks to actually generate the site.
The only part is to write the code and documentation.
The Java code in question uses Javadoc style comments to denote API documentation.
To start, simply add the following to your pom.xml file within the plugins section.

```
<plugin>
    <groupId>io.github.javaeden.orchid</groupId>
    <artifactId>orchid-maven-plugin</artifactId>
    <version>${orchid.version}</version>

    <!-- Add an Orchid Bundle. OrchidAll comes with all official themes included.
            You must include a theme separately when using the OrchidBlog bundle.
            Any additional plugins may be added as dependencies here as well. -->
    <dependencies>
        <dependency>
            <groupId>io.github.javaeden.orchid</groupId>
            <artifactId>OrchidAll</artifactId>
            <version>${orchid.version}</version>
        </dependency>
    </dependencies>

    <configuration>
        <!-- Theme is required -->
        <theme>BsDoc</theme>
        
        <!-- The following properties are optional -->
        <version>${project.version}</version>
        <baseUrl>${baseUrl}</baseUrl>                        <!-- a baseUrl prepended to all generated links. Defaults to '/' -->
        <srcDir>src/orchid/resources</srcDir>        <!-- defaults to 'src/orchid/resources' -->
        <destDir>target/docs/orchid</destDir> <!-- defaults to 'target/docs/orchid' -->
        <runTask>build</runTask>                             <!-- specify a task to run with 'mvn orchid:run' -->
    </configuration>
</plugin>
```
At the top of your pom.xml file, add the following to your properties block.
```
<orchid.version>0.16.9</orchid.version>
```
Then add the following repositories into pom.xml.
```
<pluginRepositories>
        <pluginRepository>
            <id>jcenter</id>
            <name>bintray-plugins</name>
            <url>http://jcenter.bintray.com</url>
        </pluginRepository>
        <pluginRepository>
            <id>kotlinx</id>
            <url>https://kotlin.bintray.com/kotlinx</url>
        </pluginRepository>
        <pluginRepository>
            <id>jitpack</id>
            <url>https://jitpack.io</url>
        </pluginRepository>
  </pluginRepositories>
```
Now comes configuring the site.
In this repo, the config.yaml file is already setup for a simple site.
For example purposes, here is the file.
```
site:
  about:
    siteName: Example Javadoc Site
    description: A site demonstrating Orchid's use of Java's javadoc api generation
javadoc:
  sourceDirs: ['../../main/java']
theme:
  menu:
    - type: "javadocPackages"
      title: All Packages
    - type: "pages"
```
You'll want to change the siteName key and description as per your situition.
Writing a page is fairly simple, add a markdown file to `src/orchid/resources/pages` and with the following menu configuration, the page will showup in the top navbar.
Adding java api generation is fairly straight-forward, change the sourceDirs value to whatever directory your java code is located in.