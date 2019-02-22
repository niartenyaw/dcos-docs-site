---
layout: layout.pug
navigationTitle: Login
title: Login
excerpt: Log in to your DC/OS cluster
menuWeight: 10

---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

**NOTE**: In Open DC/OS user [Authentication](1.13/security/oss/authentication/) equals `Authorization`.

Therefore, any user that logs in successfully and obtains a DC/OS Authentication token is granted full access to the cluster.

# User login

In DC/OS a user login describes the process of exchanging user credentials for a user specific [DC/OS Authentication token](/1.13/security/oss/authentication/authentication-token/).
Obtaining a DC/OS Authentication is required by any user before being able to use a DC/OS cluster. Any DC/OS Authentication tokens life-time is limited. Once the Authentication token expires the user must log in again.

DC/OS handles multiple user types. Users can be configured via the [IAM API](/1.13/security/oss/iam-api/); see [User Management](/1.13/security/oss/user-management/).

Different login methods exist for different user types but each one yields a DC/OS authentication token:

* **External user login**: An external user logs in by supplying an `OpenID Connect Token` that has been issued by Mesosphere's Auth0 instance after verification of the user credentials by an external login provider (Google, GitHub or Microsoft).
* **Local user login**: A local user logs in by supplying a `password` which is compared to the `password hash` stored inside DC/OS.
* **Service login**: A services logs in by supplying a `service login token` of which the signature is verified using the service account `public key` stored inside DC/OS.

# User logout

Users cannot log out of DC/OS. As long as an issued DC/OS Authentication tokens exists and is valid, the user that it was issued for can operate the DC/OS cluster.

There is no way to revoke access to a cluster other than to wait until the token expires.
