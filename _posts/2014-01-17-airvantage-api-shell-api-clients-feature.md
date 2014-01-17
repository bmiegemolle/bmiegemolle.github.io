---
title: Support of multiple environments in airvantage-api-shell
date_en: 2014-01-17
date_fr: 17/01/2014
layout: post
resources: ../../../resources
---

## Support of multiple environments in airvantage-api-shell

---

One of the limitations of the **airvantage-api-shell** script was that it could only be used with one of our validation platform. I've just removed this limitation, and now, the `av ssh` command enables to retrieve an access token from all AirVantage M2M Cloud platform environments.

As a reminder, the `av ssh` command syntax is the following:

> av ssh _host_

Supported production hosts are:

* na.airvantage.net
* eu.airvantage.net

The following integration and validation environments can also be accessed:

* edge.airvantage.net
* dev-airlink.airvantage.net
* qa-branch.airvantage.net
* qa-trunk.airvantage.net

![](../../../resources/img/github-32-black.png) [https://github.com/bmiegemolle/airvantage-api-shell](https://github.com/bmiegemolle/airvantage-api-shell)

Have fun!
