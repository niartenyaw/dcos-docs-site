---
layout: layout.pug
navigationTitle: Local users
title: Local users
excerpt: Managing local DC/OS user accounts
menuWeight: 20
---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

Local DC/OS user accounts can be in one of two categories:

* **Regular user account**: Regular users log in via their username and password.
* **Service account**: Services log in via a service login token generated from their corresponding RSA keypair. Service accounts exist for long running services that need to authenticate against and refresh their authentication token autonomously with DC/OS. Service accounts make it easy to automate tasks again DC/OS.
