---
layout: layout.pug
navigationTitle:  Regular users
title: Authentication tokens for regular users
excerpt: Obtaining DC/OS Authentication tokens as regular user
menuWeight: 20

---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

# Via the DC/OS CLI

**Prerequisite:**
- [DC/OS CLI](/1.13/cli/)

Using the [DC/OS CLI](/1.13/cli/) one can log in as regular DC/OS user by specifying the `dcos-users` login provider.

1. To log in to the DC/OS CLI, enter the [auth login](/1.13/cli/command-reference/dcos-auth/dcos-auth-login/) command:

```bash
dcos auth login --provider=dcos-users --username=<username> --password=<password>
```

2. Display the DC/OS authentication token by executing the following command:

```bash
dcos config show core.dcos_acs_token
```

3. Export the DC/OS Authentication token into environment for using it in other commands:
```bash
export TOKEN=$(dcos config show core.dcos_acs_token)
```

# Via the IAM API

Regular users can utilize the [Identity and Access Management (IAM) API](/1.13/security/oss/iam-api/) directly for logging in to DC/OS via HTTP. Upon login they will receive a DC/OS Authentication token.

1. To log in regular user accounts supply `<username>` and `<password>` in the following command before executing it:

```bash
curl -k -X POST https://<host-ip>/acs/api/v1/auth/login -d '{"uid": "<username>", "password": "<password>"}' -H 'Content-Type: application/json'
```

2. A DC/OS Authentication token will be returned in the HTTP response body similar to the one below:

```json
{
  "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiJib290c3RyYXB1c2VyIiwiZXhwIjoxNDgyNjE1NDU2fQ.j3_31keWvK15shfh_BII7w_10MgAj4ay700Rub5cfNHyIBrWOXbedxdKYZN6ILW9vLt3t5uCAExOOFWJkYcsI0sVFcM1HSV6oIBvJ6UHAmS9XPqfZoGh0PIqXjE0kg0h0V5jjaeX15hk-LQkp7HXSJ-V7d2dXdF6HZy3GgwFmg0Ayhbz3tf9OWMsXgvy_ikqZEKbmPpYO41VaBXCwWPmnP0PryTtwaNHvCJo90ra85vV85C02NEdRHB7sqe4lKH_rnpz980UCmXdJrpO4eTEV7FsWGlFBuF5GAy7_kbAfi_1vY6b3ufSuwiuOKKunMpas9_NfDe7UysfPVHlAxJJgg"
}
```
