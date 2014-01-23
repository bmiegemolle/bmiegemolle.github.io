---
title: Writing a Jenkins plugin / Project setup
layout: tech
resources: ../../resources
previous:
next: 02-test-your-plugin.html
---

## ![](../../resources/img/jenkins-32.png) Writing a Jenkins plugin

---

### 1. Project setup

<div style="padding-top:20px; padding-bottom:20px;">
    <b>Maven configuration</b>
</div>

First of all, it might be helpful to add the following to your `~/.m2/settings.xml`:

``` xml
<settings>
  <pluginGroups>
    <pluginGroup>org.jenkins-ci.tools</pluginGroup>
  </pluginGroups>

  <profiles>
    <!-- Give access to Jenkins plugins -->
    <profile>
      <id>jenkins</id>
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
      <repositories>
        <repository>
          <id>repo.jenkins-ci.org</id>
          <url>http://repo.jenkins-ci.org/public/</url>
        </repository>
      </repositories>
      <pluginRepositories>
        <pluginRepository>
          <id>repo.jenkins-ci.org</id>
          <url>http://repo.jenkins-ci.org/public/</url>
        </pluginRepository>
      </pluginRepositories>
    </profile>
  </profiles>
  <mirrors>
    <mirror>
      <id>repo.jenkins-ci.org</id>
      <url>http://repo.jenkins-ci.org/public/</url>
      <mirrorOf>m.g.o-public</mirrorOf>
    </mirror>
  </mirrors>
</settings>
```

<div style="padding-top:20px; padding-bottom:20px;">
    <b>Generate your plugin</b>
</div>

To start a new plugin, you can use the [Plugin Skeleton Generator](http://plugin-generator.jenkins-ci.org/), which will automatically create a skeleton for your project. It will create a `pom.xml` file and all the plugin layout, initialized with an *Hello World* sample plugin.

You can also do it in command-line with the following command:

``` sh
# You need to name your plugin here, for example "hello-world-plugin"
curl 'http://plugin-generator.jenkins-ci.org/generate?type=TAR&name=hello-world-plugin' | tar xvz
```

<div style="padding-top:20px; padding-bottom:20px;">
    <b>Import your project into Eclipse</b>
</div>

You can create the .project and .classpath files with the following command:

``` sh
mvn -DdownloadSources=true -DdownloadJavadocs=true -DoutputDirectory=target/eclipse-classes eclipse:eclipse
```

