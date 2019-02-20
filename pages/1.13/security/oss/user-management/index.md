---
layout: layout.pug
navigationTitle:  User Account Management
title: User Account Management
menuWeight: 0
excerpt: Managing DC/OS user accounts
---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

DC/OS can manage three types of user accounts:

* **External**: External users accounts are created by storing only the user ID inside DC/OS. External users log in to DC/OS by following a browser-based Single-Sign-On flow. DC/OS never receives or stores the passwords of external users. Instead, it delegates the verification of the user’s credentials to the Auth0 identity provider instance managed by Mesosphere. The Auth0 instance is configured for three login providers: Google, GitHub and Microsoft.
* **Regular**: Regular user accounts exist inside DC/OS. Users log in via their username and password stored in CockroachDB on the master nodes.
* **Service**: Service accounts credentials are stored in CockroacDB inside DC/OS.Service accounts exist for long running services that need to refresh DC/OS authentication tokens autonomously. Services log in via service login tokens. Service accounts make it easy to integrate systems with the DC/OS security architecture.

User accounts can be added via the web interface, [DC/OS CLI](/1.13/cli) or via the [IAM API](/1.13/security/oss/iam-api/) depending on the user account type.
For backwards compatibility reasons a command line script for adding external users is shipped with every DC/OS cluster.

Users can be granted access to DC/OS by another authorized user. To bootstrap this process a default external user is automatically created by the first user who logs in to the DC/OS cluster via the web interface.

<p class="message--note"><strong>NOTE: </strong>Any user with access to DC/OS can invite more users. Each DC/OS user is an administrator, there is no explicit concept of privileges with DC/OS.</p>
