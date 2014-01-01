---
title: Edit feature implemented in airvantage-api-shell
date_en: 2013-12-18
date_fr: 18/12/2013
layout: post
resources: ../../../resources
---

## Edit feature implemented in airvantage-api-shell

---

I've implemented a new feature in the **airvantage-api-shell** script: the possibility to edit entities.

The command is the following: `av vi` (see the
[README.md](https://github.com/bmiegemolle/airvantage-api-shell/blob/master/README.md) file for a complete
documentation). In a nutshell, this command first retrieves the entity details and then opens the **vi** editor to edit
them. When exiting the editor, the data will automatically be sent to the server in order to update the entity.

**Example:**

``` sh
# Edits the system with UID "c996897fa60d4882a720292171debb5a"
av vi /systems/c996897fa60d4882a720292171debb5a
```

![](../../../resources/img/github-32-black.png) [https://github.com/bmiegemolle/airvantage-api-shell](https://github.com/bmiegemolle/airvantage-api-shell)

Enjoy!