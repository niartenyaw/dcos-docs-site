---
layout: layout.pug
navigationTitle: Service Accounts
title: Service Account Management
excerpt: Managing service accounts
menuWeight: 30
---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

# Add a service account

## Using the IAM API

**Prerequisite:**
- [OpenSSL](https://www.openssl.org/)
- [DC/OS Authentication token](/1.13/security/oss/authentication/authentication-token/) exported into the environment as `TOKEN`.

A service account consists of a user ID and a RSA private key.

1. To add a service account using the DC/OS [Identity and Access Management (IAM) API](/1.13/security/oss/iam-api/) generate a RSA private key first using OpenSSL.

```bash
openssl genpkey -algorithm RSA -out private-key.pem -pkeyopt rsa_keygen_bits:2048
```

2. Extract the corresponding public key from the private key.

```bash
openssl rsa -pubout -in private-key.pem -out public-key.pem
```

3. Then replace `<service-account-id>` with the desired value in the following command and execute it:

```bash
curl -i -X PUT http://<host-ip>/acs/api/v1/users/<service-account-id> -d '{"public_key": "'"$(sed ':a;N;$!ba;s/\n/\\n/g' public-key.pem)"'", "provider_type": "internal"}' -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```

# List service accounts

## Using the IAM API

**Prerequisite:**
- [DC/OS Authentication token](/1.13/security/oss/authentication/authentication-token/) exported into the environment as `TOKEN`.

To list all configured service accounts using the DC/OS [Identity and Access Management (IAM) API](/1.13/security/oss/iam-api/) execute the following command:

```bash
curl -i -X GET http://<host-ip>/acs/api/v1/users\?type\=service -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```

# Change a service account public key

## Using the IAM API

**Prerequisite:**
- [DC/OS Authentication token](/1.13/security/oss/authentication/authentication-token/) exported into the environment as `TOKEN`.

To change a service account's public key using the DC/OS [Identity and Access Management (IAM) API](/1.13/security/oss/iam-api/) supply a new public key in the `public-key.pem` file. Then replace `<service-account-id>` in the following command and execute it:

```bash
curl -i -X PATCH http://<host-ip>/acs/api/v1/users/<service-account-id> -d '{"public_key": "'"$(sed ':a;N;$!ba;s/\n/\\n/g' public-key.pem)"'", "provider_type": "internal"}' -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```

# Remove a service account

## Using the IAM API

**Prerequisite:**
- [DC/OS Authentication token](/1.13/security/oss/authentication/authentication-token/) exported into the environment as `TOKEN`.

To remove a local user account using the DC/OS [Identity and Access Management (IAM) API](/1.13/security/oss/iam-api/) replace `<username>` with the corresponding value and execute the following command:

```bash
curl -i -X DELETE http://<host-ip>/acs/api/v1/users/<service-account-id> -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```
