---
layout: layout.pug
navigationTitle: Local User Accounts
title: Local User Account Management
excerpt: Managing local user accounts
menuWeight: 20
---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

# Add a local user account

## Using the IAM API

**Prerequisite:**
- [DC/OS Authentication token](/1.13/security/oss/authentication/authentication-token/) exported into the environment as `TOKEN`.

To add a local user account using the DC/OS [Identity and Access Management (IAM) API](/1.13/security/oss/iam-api/) replace `<uid>` and `<password>` with the corresponding values and execute the following command:

```bash
curl -i -X PUT http://<host-ip>/acs/api/v1/users/<uid> -d '{"password": "<password>"}' -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```

**NOTE**: The password must be at least 5 characters long.

# List local user accounts

## Using the IAM API

**Prerequisite:**
- [DC/OS Authentication token](/1.13/security/oss/authentication/authentication-token/) exported into the environment as `TOKEN`.

To list all configured user accounts using the DC/OS [Identity and Access Management (IAM) API](/1.13/security/oss/iam-api/) execute the following command:

```bash
curl -i -X GET http://<host-ip>/acs/api/v1/users -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```

**NOTE**: This will include external user accounts. Local user accounts are listed as `provider_type: internal`.

# Change a local user password

## Using the IAM API

**Prerequisite:**
- [DC/OS Authentication token](/1.13/security/oss/authentication/authentication-token/) exported into the environment as `TOKEN`.

To change a local user account's password using the DC/OS [Identity and Access Management (IAM) API](/1.13/security/oss/iam-api/) replace `<uid>` and `<password>` with the corresponding values and execute the following command:

```bash
curl -i -X PATCH http://<host-ip>/acs/api/v1/users/<uid> -d '{"password": "<password>"}' -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```

**NOTE**: The password must be at least 5 characters long.

# Remove a local user account

## Using the IAM API

**Prerequisite:**
- [DC/OS Authentication token](/1.13/security/oss/authentication/authentication-token/) exported into the environment as `TOKEN`.

To delete a local user account using the DC/OS [Identity and Access Management (IAM) API](/1.13/security/oss/iam-api/) replace `<uid>` with the corresponding value and execute the following command:

```bash
curl -i -X DELETE http://<host-ip>/acs/api/v1/users/<uid> -H 'Content-Type: application/json' -H "Authorization: token=$TOKEN"
```

## Using the web interface

1. Log in to the web interface.
2. From the **Users** screen, select the uid and click **Delete**.
3. Click **Delete** to confirm the action.
