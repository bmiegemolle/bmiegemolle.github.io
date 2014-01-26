---
title: Writing a Jenkins plugin / Test your plugin
layout: tech
resources: ../../resources
previous: 01-project-setup.html
next: 03-deploy-your-plugin.html
---

## ![](../../resources/img/jenkins-32.png) Writing a Jenkins plugin

---

### 2. Test your plugin

You can test your plugin in a dynamic Jenkins instance with a simple Maven command:

``` sh
export MAVEN_OPTS="-Xdebug -Xrunjdwp:transport=dt_socket,server=y,address=8000,suspend=n"
mvn hpi:run
```

This Jenkins instance is accessible at [http://localhost:8080/jenkins](http://localhost:8080/jenkins). Note that you can change the port by adding the `-Djetty.port` option:

``` sh
mvn hpi:run -Djetty.port=8090
```

The `MAVEN_OPTS` environment variable launches this whole thing with the debugger port 8000, so you should be able to start a debug session to this port from your IDE.

If you look at the content of your plugin folder, you'll see a `work` directory with the installation of this Jenkins instance. This folder should be excluded from your version control system.

