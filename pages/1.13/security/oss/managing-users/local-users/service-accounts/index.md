---
layout: layout.pug
navigationTitle: Service accounts
title: Service accounts
excerpt: Managing regular user accounts
menuWeight: 20
---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

By default no service accounts exist in DC/OS. The only way to add service accounts is via the DC/OS [Identity and Access Management (IAM) API](/1.13/security/oss/iam-api/).

# Manage service accounts via the IAM API

The DC/OS [IAM API](/1.13/security/oss/iam-api/) allows for managing the full life-cycle of service accounts.

## Obtain a DC/OS authentication token

**Prerequisite:**
- [DC/OS CLI](/1.13/cli/)

To interact with the IAM users API, it is required to authenticate first against the DC/OS cluster. This example assumes that a valid DC/OS authentication token has been obtained by logging in first as an [external user](/1.13/security/oss/managing-users/external-users/) via the [DC/OS CLI](/1.13/cli/). The token can then be exported into the environment.

```bash
export TOKEN=$(dcos config show core.dcos_acs_token)
```

## Add service accounts via the IAM API

**Prerequisite:**
- [OpenSSL](https://www.openssl.org/)

A service account consists of a user ID and a RSA keypair.

1. To add a service account generate a RSA private key first using OpenSSL.

```bash
openssl genrsa -des3 -out private-key.pem 2048
```

2. Extract the corresponding public key from the private key.
```bash
openssl rsa -in private-key.pem -outform PEM -pubout -out public-key.pem
```

replace `<username>` and `<password>` with the corresponding values and execute the following command:

```bash
curl -i -X PUT https://<host-ip>/acs/api/v1/users/<username> -d '{"public_key": "<public-key>", "provider_type": "internal"}' -H 'Content-Type: application/json' -H 'Authorization: token=$TOKEN'
```

## Update regular user accounts via the IAM API

## Delete regular user accounts via the IAM API

To delete a regular user account replace `<username>` with the corresponding value and execute the following command:

```bash
curl -i -X DELETE https://<host-ip>/acs/api/v1/users/<username> -H 'Content-Type: application/json' -H 'Authorization: token=$TOKEN'
```

# Log in regular users via the DC/OS CLI 

**Prerequisite:**
- [DC/OS CLI](/1.13/cli/)


Using the [DC/OS CLI](/1.13/cli/) one can log in as regular DC/OS user by specifying the `dcos-users` login provider.

To log in to the DC/OS CLI, enter the [auth login](/1.13/cli/command-reference/dcos-auth/dcos-auth-login/) command:

```bash
dcos auth login --provider=dcos-users --username=<username> --password=<password>
```

# Switch users 

To switch users, you must log out of the current user and then back in as the new user.

### From the DC/OS CLI

To log out of the DC/OS CLI, enter the command:

```bash
dcos config unset core.dcos_acs_token
Removed [core.dcos_acs_token]
```

You can now log in as another user.
