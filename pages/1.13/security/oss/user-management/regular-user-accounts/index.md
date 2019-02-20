---
layout: layout.pug
navigationTitle: Regular user accounts
title: Managing regular user accounts
excerpt: Managing regular user accounts
menuWeight: 20
---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

By default no regular user account exists in DC/OS. The only way to add regular user accounts is via the DC/OS [Identity and Access Management (IAM) API](/1.13/security/oss/iam-api/).

**NOTE**: Currently, regular users cannot log in to DC/OS via the web interface.

# Manage regular user accounts via the IAM API

**Prerequisite:**
- [DC/OS Authentication token](/1.13/security/oss/authentication/obtaining-auth-tokens/)

The DC/OS [IAM API](/1.13/security/oss/iam-api/) allows for managing the full life-cycle of regular user accounts.

## Add regular user accounts via the IAM API

To add a regular user account replace `<username>` and `<password>` with the corresponding values and execute the following command:

```bash
curl -ki -X PUT https://<host-ip>/acs/api/v1/users/<username> -d '{"password": "<password>"}' -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```

**NOTE**: Passwords must be at least 5 characters long.

## Update regular user accounts via the IAM API

To add a regular user account replace `<username>` and `<new-password>` with the corresponding values and execute the following command:

```bash
curl -ki -X PATCH https://<host-ip>/acs/api/v1/users/<username> -d '{"password": "<new-password>"}' -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```

## Delete regular user accounts via the IAM API

To delete a regular user account replace `<username>` with the corresponding value and execute the following command:

```bash
curl -ki -X DELETE https://<host-ip>/acs/api/v1/users/<username> -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```
