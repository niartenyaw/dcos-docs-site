---
layout: layout.pug
navigationTitle:  User Account Management
title: User Account Management
menuWeight: 10
excerpt: Managing DC/OS user accounts
---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

DC/OS is designed as a multi-user system.

Open DC/OS can handle three types of user accounts:

* **External user accounts**: External user accounts exist for users who want to use their Google, GitHub, or Microsoft credentials. DC/OS does never receive or store the passwords of external users.
* **Local user accounts**: Local user accounts exist for users who want to create a user account within DC/OS. Usernames and password hashes are stored in CockroachDB on the master nodes.
* **Service accounts**: Service accounts exist for long-running services that need to refresh authentication tokens autonomously. Public key information is stored per service in CockroachDB within DC/OS.

User accounts can be managed by any authorized user. To bootstrap this process, in Open DC/OS a default external user is automatically created by the first user who logs in via the web interface.

<p class="message--note"><strong>NOTE: </strong>Any user with access to Open DC/OS can create more user accounts. Each user account in Open DC/OS is an authorized administrator account, there is no explicit concept of privileges with Open DC/OS.</p>
