---
layout: layout.pug
navigationTitle:  User Account Management
title: User Account Management
menuWeight: 30
excerpt: Managing DC/OS user accounts
---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

DC/OS is designed as a multi-user system.

Open DC/OS can handle three types of user accounts:

* **External user accounts**: External user accounts exist for users who want to login with their Google, GitHub, or Microsoft credentials. The DC/OS cluster does not receive or store the passwords of external users.
* **Local user accounts**: Local user accounts exist for users who want to create a new user account inside DC/OS. Local users' usernames and password hashes are stored in CockroachDB on the master nodes.
* **Service accounts**: Service accounts exist for long-running services that want to refresh DC/OS authentication tokens autonomously. Therefore public key information is stored per service in CockroachDB inside DC/OS.

External users can be added through the web interface or the `dcos_add_user.py` script. Local users can only be added through the API.

User accounts can be managed by any authorized user. To bootstrap this process, in Open DC/OS a default external user is automatically created by the first user who logs in via the web interface.

<p class="message--note"><strong>NOTE: </strong>Any user with access to Open DC/OS can invite more users. Each Open DC/OS user is an administrator, there is no explicit concept of privileges with Open DC/OS.</p>
