---
layout: layout.pug
excerpt: Managing security in your datacenter using DC/OS Open Source
title: DC/OS Open Source Security
menuWeight: 80
---
<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

Ensure the network is setup according to the information for [securing your cluster](/1.13/administering-clusters/securing-your-cluster/).

Authentication in DC/OS is implemented via dedicated a DC/OS Authentication token.

DC/OS uses the JSON Web Token (JWT) format for its authentication tokens. JWT is an open, industry standard ([RFC
7519](https://tools.ietf.org/html/rfc7519)) method for securely representing claims between two parties.

To log in out-of-the-box DC/OS has an OpenID Connect 1.0 endpoint configured at [dcos.auth0.com](https://dcos.auth0.com/.well-known/openid-configuration) (in cooperation with [Auth0](https://auth0.com/)) with connections to Google, GitHub, and Microsoft to provide basic authentication for DC/OS installations.

![Auth0 badge](/1.13/img/a0-badge-light.png)

All access management in DC/OS is done via the DC/OS Identity and Access Manager (IAM). This includes user account management, login as well as authentication token distribution. The IAM provides an HTTP API for managing user accounts in a RESTful fashion.

DC/OS Authentication tokens can be obtained using [OpenID Connect 1.0](https://openid.net/specs/openid-connect-core-1_0.html), which is a simple identity layer built on top of the [OAuth 2.0](http://oauth.net/2/) protocol.

Additionally, local user and service accounts can be configured for logging in without external dependencies and for automating authentication against the cluster in a secure manner.

# Further reading

- [Let’s encrypt DC/OS!](https://mesosphere.com/blog/2016/04/06/lets-encrypt-dcos/):
  a blog post about using [Let's Encrypt](https://letsencrypt.org/) with
  services running on DC/OS.

# Future work

We are looking forward to working with the DC/OS community on improving existing
security features as well as on introducing new ones in the coming releases.

# Next Steps

- [Understand DC/OS security](/1.13/administering-clusters/)
- [Learn how to monitor a DC/OS cluster](/1.13/monitoring/)
