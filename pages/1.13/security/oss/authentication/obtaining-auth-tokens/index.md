---
layout: layout.pug
navigationTitle: Obtaining Authentication Tokens
title: Obtaining DC/OS Authentication Tokens
excerpt: Obtaining DC/OS Authentication Tokens
menuWeight: 10

---
<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

DC/OS use a JSON Web Tokens (JWT) named `DC/OS authentication token` for the purpose of authenticating users against the cluster.

DC/OS authentication tokens can be obtained by any registered user of the cluster. The way to obtain a DC/OS authentication involves logging in to the cluster but varies slightly by user type.

DC/OS uses JSON Web Tokens (JWT) for the purpose of authenticating HTTP requests against the cluster. DC/OS authentication tokens are sent via HTTP in the `Authorization` header. The `Authorization` header value must be in the format: `token=<token>`. Other formats like `Bearer <token>` are not supported.

From the [DC/OS CLI](/1.13/cli), you can log in to your cluster which results in obtaining a DC/OS authentication token. The token will then be used for authenticating the logged in on subsequent DC/OS CLI commands. 

## <a name="log-in-cli"></a>Authenticating through DC/OS CLI

Authentication is only supported for DC/OS CLI version 0.4.3 and later. See [here](/1.13/cli/update/) for upgrade instructions.

The DC/OS CLI stores the token in a configuration file in the `.dcos` directory under the home directory of the user running the CLI. This token can be used with the `curl` command to access DC/OS APIs, using `curl` or `wget`. For example, `curl -H 'Authorization: token=<token>' http://cluster`.


You can make external calls to HTTP API endpoints in your DC/OS cluster. You must first obtain an authentication token and then include it in your HTTP request. Authentication tokens expire after five days. You can see the expiration time in the ["exp" (Expiration Time) Claim](https://tools.ietf.org/html/rfc7519#section-4.1.4) of the JSON Web Token (JWT). Refresh your token by re-logging in to DC/OS.

# Obtaining an authentication token

Obtain your authentication token using the DC/OS CLI. When you log into the DC/OS CLI, you paste an OpenID Connect ID token into your terminal prompt. This OpenID Connect ID token logs you into the DC/OS CLI, but does not allow you to access the HTTP API endpoints. You must obtain an authentication token to gain access to the HTTP API endpoints. Complete the following steps to obtain your authentication token.

1. [Log in to the DC/OS CLI](/1.13/security/oss/managing-authentication/#logging-in-to-the-dcos-cli). Logging into the DC/OS CLI causes your authentication token to be written to a configuration file. 

2. Use the following command to confirm that this write succeeded, and to view your authentication token.

```bash
dcos config show core.dcos_acs_token
```

# Passing your authentication token to DC/OS endpoints

DC/OS endpoints expect to find your authentication token in the `Authorization` field of your HTTP header as follows.

```http
Authorization: token=<authentication-token>
```

With `cURL`, you can use command substitution to extract the token value from your configuration file. The following examples illustrate this syntax.

**Sample Marathon request:**

```bash
curl --header "Authorization: token=$(dcos config show core.dcos_acs_token)" http://<master-host-name>/service/marathon/v2/apps
```

**Sample Mesos request:**

```bash
curl --header "Authorization: token=$(dcos config show core.dcos_acs_token)" http://<master-host-name>/mesos/master/state.json
```
