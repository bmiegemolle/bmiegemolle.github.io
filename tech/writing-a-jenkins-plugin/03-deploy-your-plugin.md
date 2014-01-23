---
title: Writing a Jenkins plugin / Project setup
layout: tech
resources: ../../resources
previous: 02-test-your-plugin.html
---

## ![](../../resources/img/jenkins-32.png) Writing a Jenkins plugin

---

### 3. Deploy your plugin

If you want to deploy your plugin into a real Jenkins instance, you first need to package it:

``` sh
mvn package
```

This will produce a `target/hello-world.hpi` file. You can now deploy your custom plugin into an existing Jenkins by following the following steps:

1. Stop Jenkins
2. Remove the previous version of your plugin if this is not the first time you're deploying it: `rm -rf $JENKINS_HOME/plugins/hello-world*`
3. Copy the `hello-world.hpi` file to `$JENKINS_HOME/plugins` directory
4. Start Jenkins

