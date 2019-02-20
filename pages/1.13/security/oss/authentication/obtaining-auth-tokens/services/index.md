---
layout: layout.pug
navigationTitle:  Services
title: Authentication tokens for services
excerpt: Obtaining DC/OS Authentication tokens as service
menuWeight: 30

---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

Service accounts are used in conjunction with public-private key pairs, secrets, permissions, and authentication tokens to provide access for DC/OS [services](/1.13/overview/concepts/#dcos-service) to DC/OS. Service accounts control the communications and DC/OS API actions that the services are permitted to make.

DC/OS services require authentication depending on your security mode.

| Security mode | Intracluster communication | External cluster communication |
|---------------|-----------------------|----------------------------|
| Permissive    | Optional              | Required                   |
| Strict        | Required              | Required                   |

## Service Authentication Components
To authenticate a service, you will need:

-  Public-private key pair
-  Service account
-  Secret for service account
-  Permissions for service account
-  Service login token

### JSON Web Tokens (JWT)
Service authentication involves two JSON Web Tokens (JWT) for service authentication.

-  **Service Login token** To log in to DC/OS, a **service login token** is required. It is a JWT signed with the service's private key, and serves as a one-time password. A service login token should be generated for one-time usage (for example, for a single service login procedure) and should include an expiration.

-  **Authentication token** After a service connects to DC/OS with the service login token, the IAM service creates an *authentication token* which the service can then use to authenticate its outgoing requests to DC/OS. An authentication token can be used for long-term access.

### Mesos Authentication Principal
DC/OS services supply a principal when they register with the Mesos masters. In [strict security mode](/1.13/security/ent/#security-modes), the service account name must match the name specified in the `principal`. For more information about principals, see the [Mesos documentation](http://mesos.apache.org/documentation/latest/authorization/).

The following diagram illustrates this sequence.

![Service authentication](/1.13/img/authn-service.png)

Figure 1. Service authentication

# Refreshing Tokens
Services can use a variety of means to refresh their tokens. Ideally, a service should calculate the length of time until the token expires, which is embedded within the token itself, and request a new one before it expires. However, a service can also wait until it receives a `401` to request a new token.

You may need to provision a service with a service account depending on your [security mode](/1.13/security/ent/#security-modes) and the origin of the service's requests. 

An API consumer should be able to handle when its current authentication token expires.

-  **Post-Expiration Renewal** With this method, you obtain a new auth token after an "invalid token" response is received. An invalid authentication token is responded to with a 401 HTTP status code and the service re-invokes the service account login procedure. It attempts to get a fresh authentication token (with retry and back-off). During the period where the service has no valid authentication token, the service might need to hold back operations, resulting in latency spikes.
- **Pre-Expiration Renewal** With this method, the token is refreshed before it expires. The service can schedule asynchronous token renewal ahead of the expiration. It can fetch a new authentication token while the old one is still valid. This prevents the latency spikes caused by an expired authentication token.
