---
layout: layout.pug
navigationTitle: Local users
title: Local users
excerpt: Managing local DC/OS user accounts
menuWeight: 20
---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

Local DC/OS user accounts can be in one of two categories:

* **Regular user accounts**: Regular users log in via their username and password.
* **Service accounts**: Services log in via a service login token. Service accounts exist for long running services that need to refresh their DC/OS authentication token autonomously. Service accounts make it easy to integrate systems with the DC/OS security architecture.
