---
layout: layout.pug
navigationTitle:  External users
title: Authentication tokens for external users
excerpt: Obtaining DC/OS Authentication tokens as external user
menuWeight: 10

---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

# Via the DC/OS CLI

**Prerequisite:**
- [DC/OS CLI](/1.13/cli/)

1.  To log in to the DC/OS CLI, enter the [auth login](/1.13/cli/command-reference/dcos-auth/dcos-auth-login/) command:

```bash
dcos auth login --provider dcos-oidc-auth0
If your browser didn't open, please go to the following link:

    http://172.17.0.2/login?redirect_uri=urn:ietf:wg:oauth:2.0:oob

Enter OpenID Connect ID Token: 
>
```

2. Follow the displayed instructions to trigger the browser login flow.

3. Copy the `OpenID Connect ID token` from the modal dialog that appears in the browser.

4. Paste the `OpenID Connect ID token` into the DC/OS CLI for login completion.

**NOTE**: The `--provider` argument is set to `dcos-oidc-auth0` by default.

5. Display the DC/OS authentication token by executing the following command:

```bash
dcos config show core.dcos_acs_token
```
6. Export the DC/OS Authentication token into environment for using it in other commands:
```bash
export TOKEN=$(dcos config show core.dcos_acs_token)
```

# Via the web interface

1.  Launch the DC/OS web interface.
2.  Log in through a single sign-on flow using the identity provider of your choice (Google, GitHub, and Microsoft).

**NOTE**: The Single-Sign-On flow will result in the DC/OS Authentication token being stored in a browser cookie.
