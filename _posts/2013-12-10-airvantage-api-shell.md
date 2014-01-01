---
title: AirVantage API access from Shell command-line
date_en: 2013-12-10
date_fr: 10/12/2013
layout: post
resources: ../../../resources
---

## AirVantage API access from Shell command-line

---

I've started a sample project to show how to access AirVantage API using a Shell script.

![](../../../resources/img/github-32-black.png) [https://github.com/bmiegemolle/airvantage-api-shell](https://github.com/bmiegemolle/airvantage-api-shell)

The **airvantage-api-shell** project aims to provides a light and flexible Shell script that enables to interact with
AirVantage M2M Cloud API in command-line. The
[README.md](https://github.com/bmiegemolle/airvantage-api-shell/blob/master/README.md) file provides a complete
documentation about what the script does. In a nutshell, the following commands are available:

* `av ssh` retrieves an access token, and stores it in a /tmp file used by further *av* commands
* `av whoami` displays the details of the user associated with the current access token
* `av ls` enables to list entities
* `av find` enables to find a specific entity
* `av cat` displays the details of a specific entity

**Examples:**

``` sh
# Retrieve an access token to the North America datacenter
av ssh na.airvantage.net

# Know who I am
av whoami

# List all systems, and display them as a list of JSON objects
av ls /systems

# List all users, and display them as a list of plain text UIDs
av ls /users --uid-only

# Find systems with a commStatus equals to "ERROR", and display them as a list of JSON objects
av find -commStatus ERROR /systems

# Find operations created by the user "administrator@m2mop.net", and display them as a list of JSON objects
av find -user administrator@m2mop.net /operations

# Displays the details of the system with UID "c996897fa60d4882a720292171debb5a"
av cat /systems/c996897fa60d4882a720292171debb5a

# Displays the details of all systems with a commStatus equals to "ERROR"
av find -commStatus ERROR --uid-only | av cat
```

**Known limitations**

1. OAuth API client informations (client ID and secret key) are both hard-coded in the `av` script. This API client only exists on our validation platform. Those informations should actually be asked by the _av ssh_ command.
2. All `av` commands only work with API that return a list of items identified by a UID (unique identifier). It does not work with other entities, such as labels.
3. Pagination is not handled yet by the `av` script. Default pagination will thus be used when accessing to any API (i.e. no offset, and up to 100 items returned).

**What's coming next?**

Two main topics should be addressed soon:

1. Remove the limitations described above.
2. Implement commands to create, edit or remove entities.

---

<div class="panel panel-default">
    <div class="panel-heading">
        <strong>What is AirVantage ?</strong><br/><br/>
        Do you know about the AirVantage M2M Cloud platform? In a few word, this is a platform we're developing at
        Sierra Wireless, which enables to manage a fleet of remote machines. For more details, please go to
        <a href="http://airvantage.net">http://airvantage.net</a>.<br/><br/>
        The AirVantage M2M Cloud platform comes with a RESTful API that exposes all AirVantage features to developers.
        The goal of the <a href="https://github.com/bmiegemolle/airvantage-api-shell">airvantage-api-shell</a> project
        is to show how to play with it!
    </div>
</div>