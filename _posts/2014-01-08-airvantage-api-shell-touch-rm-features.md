---
title: New features available in airvantage-api-shell
date_en: 2014-01-08
date_fr: 08/01/2014
layout: post
resources: ../../../resources
---

## New features available in airvantage-api-shell

---

I've implemented two new features in the **airvantage-api-shell** script.

#### Entity creation

The `av touch` command enables to create entities. The `vi` editor is used to enter the entity fields values. When exiting the editor, those information are sent to the server in order to create the entity. There are two creation modes:

* **Creation from scratch:** The `vi` editor is opened with an empty JSON content. You'll need to provide all necessary information to create the entity.
* **Creation from template:** You can use an existing entity as a template, by specifying its UID in the command line arguments. In this case, a first request is done to the server in order to get the entity details. The `vi` editor is then opened with those details. All you have to do is editing the information to match your new entity values.

#### Entity deletion

This can be done with the `av rm` command. Be careful: no confirmation will be prompted before actually deleting the entity. You should be sure of what you're doing when invoking this command!

---

As usual, the complete documentation of these features can be found in the
[README.md](https://github.com/bmiegemolle/airvantage-api-shell/blob/master/README.md) file of the project.

**Examples:**

``` sh
# Creates a system from scratch
av touch /systems

# Creates a gateway using the gateway with UID "590fea92135a46e9acc7b59952843ec9" as a template
av touch /gateways --template-uid 590fea92135a46e9acc7b59952843ec9

# Deletes the system with UID "c996897fa60d4882a720292171debb5a"
av rm /systems/c996897fa60d4882a720292171debb5a
```

![](../../../resources/img/github-32-black.png) [https://github.com/bmiegemolle/airvantage-api-shell](https://github.com/bmiegemolle/airvantage-api-shell)

