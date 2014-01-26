---
title: Writing a Jenkins plugin / Extension points
layout: tech
resources: ../../resources
previous: 03-deploy-your-plugin.html
next: 05-conclusion.html
---

## ![](../../resources/img/jenkins-32.png) Writing a Jenkins plugin

---

### 4. Extension points

Jenkins provides a [set of extension points](https://wiki.jenkins-ci.org/display/JENKINS/Extension+points), which are interfaces or abstract classes that model a part of a Jenkins functionality. Plugins can extend those extention points in order to contribute with their implementation. They can also define their own extension points.

The incredible huge amount of open source plugins available in the [Jenkins GitHub account](https://github.com/jenkinsci) provide many exemples that can get you started to create your own plugin.

I'll describe here a couple of extension points I use in my new [Git build data plugin](https://github.com/bmiegemolle/git-build-data-plugin).

<div style="padding-top:20px; padding-bottom:20px;">
    <b>List view column</b>
</div>

This extension point can be used to add a new column in the job list view (see [LastBuildBranch.java](https://github.com/bmiegemolle/git-build-data-plugin/blob/master/src/main/java/jenkins/plugins/gitbuilddata/LastBuiltBranch.java)). The column view is rendered by the [column.jelly](https://github.com/bmiegemolle/git-build-data-plugin/blob/master/src/main/resources/jenkins/plugins/gitbuilddata/LastBuiltBranch/column.jelly) file.

In order to bind the Jelly file to the Java class, the path of the Jelly file must correspond to the complete qualified name of the Java class. For exemple:

* Java class: `jenkins.plugins.gitbuilddata.LastBuiltBranch` (path: `src/main/java/jenkins/plugins/gitbuilddata/LastBuiltBranch.java`)
* Jelly file: `src/main/resources/jenkins/plugins/gitbuilddata/LastBuiltBranch/column.jelly`

Now, we should have a look at the content of the [column.jelly](https://github.com/bmiegemolle/git-build-data-plugin/blob/master/src/main/resources/jenkins/plugins/gitbuilddata/LastBuiltBranch/column.jelly) file:

```
<j:jelly xmlns:j="jelly:core">
    <td>${it.getLastBuiltBranch(job)}</td>
</j:jelly>
```

Many things can be noted here:

1. The `job` variable is automatically passed to the Jelly file. It contains the item to render.
2. As the Jelly file is tied directly to the Java class, we can call any method on this class. The keyword `it` enables to get a reference to it.
3. The Jelly file renders the `<td>` tag, as mentioned in the [ListViewColumn Javadoc](http://javadoc.jenkins-ci.org/?hudson/views/ListViewColumn.html).

Concretely, the rendering of the item view is delegated to the `getLastBuiltBranch` method of the [LastBuildBranch](https://github.com/bmiegemolle/git-build-data-plugin/blob/master/src/main/java/jenkins/plugins/gitbuilddata/LastBuiltBranch.java) class:

``` java
public String getLastBuiltBranch(@SuppressWarnings("rawtypes") Job job) {
    try {
        BuildData buildData = job.getLastBuild().getAction(BuildData.class);
        if (buildData.getLastBuiltRevision().getBranches().size() != 1) {
            return "N/A";
        } else {
            return buildData.getLastBuiltRevision().getBranches().iterator().next().getName();
        }
    } catch (Exception e) {
        return "N/A";
    }
}
```

A second Jelly file named [columnHeader.jelly](https://github.com/bmiegemolle/git-build-data-plugin/blob/master/src/main/resources/jenkins/plugins/gitbuilddata/LastBuiltBranch/columnHeader.jelly) is used to render the column header. If this file didn't existed, the framework would have defaulted to the use of the `getColumnCaption()` method to render it.

<div style="padding-top:20px; padding-bottom:20px;">
    <b>Prominent project action</b>
</div>

A prominent object action is an action displayed at the top of a job page (just like the test result trend graph).

Two Java class must be defined:

* the [BuiltBranchesProjectAction](https://github.com/bmiegemolle/git-build-data-plugin/blob/master/src/main/java/jenkins/plugins/gitbuilddata/BuiltBranchesProjectAction.java) class, which defines the action,
* the [BuiltBranchesProjectActionFactory](https://github.com/bmiegemolle/git-build-data-plugin/blob/master/src/main/java/jenkins/plugins/gitbuilddata/BuiltBranchesProjectActionFactory.java) class, which is the extension point that enables to insert actions into projects. This factory will be responsible of instantiating our action:

```java
@Override
public Collection<? extends Action> createFor(AbstractProject target) {
    return Collections.singleton(new BuiltBranchesProjectAction(target));
}
```

The view of our action is rendered by the [floatingBox.jelly](https://github.com/bmiegemolle/git-build-data-plugin/blob/master/src/main/resources/jenkins/plugins/gitbuilddata/BuiltBranchesProjectAction/floatingBox.jelly) file:

```
<j:jelly xmlns:j="jelly:core">
    <j:if test="${from.isGitProject()}">
        <div style="padding:30px">
            <table style="padding-bottom:15px;">
                <tr>
                    <td><img src="${rootURL}/plugin/git-build-data/git.png"/></td>
                    <td><h1 style="padding-left:20px;">Built branches</h1></td>
                </tr>
            </table>
            <j:forEach var="branch" items="${from.getBuiltBranches()}">
                <img src="${resURL}/images/32x32/${branch.getBuildStatus()}"/>
                <a href="${rootURL}/${branch.getBuildUrl()}" style="padding-left:10px;">
                    #${branch.getBuildNumber()}
                </a> - <b>${branch.getBranchName()}</b><br/>
            </j:forEach>
            </div>
    </j:if>
</j:jelly>
```

Here, the class implementing the action can be referenced by the `from` variable. As the `BuiltBranchesProjectAction.getBuiltBranches()` method returns a `List` object, we can use the Jelly tag `foreach` to iterate over the returned list.

A summary of all Jelly tag libraries can be found in the [Jelly tag documentation](http://commons.apache.org/proper/commons-jelly/tags.html).
