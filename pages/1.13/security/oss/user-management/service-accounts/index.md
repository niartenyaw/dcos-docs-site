---
layout: layout.pug
navigationTitle: Service accounts
title: Managing service accounts
excerpt: Managing service accounts
menuWeight: 20
---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

By default no service account exists in DC/OS. The only way to add service accounts is via the DC/OS [Identity and Access Management (IAM) API](/1.13/security/oss/iam-api/).

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
openssl genpkey -algorithm RSA -out private-key.pem -pkeyopt rsa_keygen_bits:2048
```

2. Extract the corresponding public key from the private key.

```bash
openssl rsa -pubout -in private-key.pem -out public-key.pem
```

3. Then replace `<service-account-id>` with the corresponding value in the following command and execute it:

```bash
curl -ki -X PUT https://<host-ip>/acs/api/v1/users/<service-account-id> -d '{"public_key": "'"$(sed ':a;N;$!ba;s/\n/\\n/g' public-key.pem)"'", "provider_type": "internal"}' -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```

## List service accounts via the IAM API

To list all configured service accounts execute the following command:

```bash
curl -ki -X GET https://<host-ip>/acs/api/v1/users\?type\=service -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```

## Update service accounts via the IAM API

To update a service account supply the new public key in the `new-public-key.pem` file. Then replace `<service-account-id>` in the following command and execute it:

```bash
curl -ki -X PATCH https://<host-ip>/acs/api/v1/users/<service-account-id> -d '{"public_key": "'"$(sed ':a;N;$!ba;s/\n/\\n/g' new-public-key.pem)"'", "provider_type": "internal"}' -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```

## Delete service accounts via the IAM API

To delete a regular user account replace `<username>` with the corresponding value and execute the following command:

```bash
curl -ki -X DELETE https://<host-ip>/acs/api/v1/users/<service-account-id> -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```

# Log in service accounts via the DC/OS CLI 

**Prerequisite:**
- [DC/OS CLI](/1.13/cli/)

Using the [DC/OS CLI](/1.13/cli/) one can log in as DC/OS service account by specifying the `dcos-services` login provider.

To log in to the DC/OS CLI, enter the [auth login](/1.13/cli/command-reference/dcos-auth/dcos-auth-login/) command by specifying `<service-account-id>` and `<private-key-path>` corresponding to the service account:

```bash
dcos auth login --provider=dcos-users --username=<service-account-id> --private-key=<private-key-path>
```

# Switch users 

To switch users, you must log out of the current user and then back in as the new user.

### From the DC/OS CLI

To log out of the DC/OS CLI, enter the command:

```bash
dcos auth logout
```

You can now log in as another user.
