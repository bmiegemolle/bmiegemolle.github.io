---
title: Git build data plugin and Technical notes
date_en: 2014-01-26
date_fr: 26/01/2014
layout: post
resources: ../../../resources
---

## Git build data plugin and Technical notes

---

<div style="padding-top:20px; padding-bottom:20px;">
    <b>Git build data plugin</b>
</div>

I've started the development of a new Jenkins plugin, named **Git build data plugin**.

In Jenkins, jobs that are configured to build multiple Git branches actually builds one branch at a time, meaning that each build corresponds to one and only one branch. For such jobs, it's quite hard to know the build status of each branch.

This Jenkins plugin answers the following questions :

* In the job list, which is the last branch that has been built for each job?
* For a particular job, what is the build status of each branch?


![](../../../resources/img/github-32-black.png) [https://github.com/bmiegemolle/git-build-data-plugin](https://github.com/bmiegemolle/git-build-data-plugin)

---

<div style="padding-top:20px; padding-bottom:20px;">
    <b>Technical notes</b>
</div>

I've also added a new **Technical notes** section to my home page, which contains tips, snippets or tutorials about various things, such as Jenkins plugin development or Android software development.

![](../../../resources/img/tech-32.png) [Technical notes](../../../tech.html)
