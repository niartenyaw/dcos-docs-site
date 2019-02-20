---
layout: layout.pug
navigationTitle:  Authentication
title: Authentication
excerpt: Authenticating users against DC/OS
menuWeight: 20

---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

DC/OS provides authentication mechanisms for users in its user database to identify themselves.

Different DC/OS user types can be configured via the [IAM API](/1.13/security/oss/iam-api/); see [User Management](/1.13/security/oss/user-management/).

Identification of users is enforced by Admin Router which authenticates users based on information from the DC/OS [Identity and Access Manager (IAM)](/1.13/overview/architecture/components/#dcos-iam). 

Other authenticators can authenticate users on behalf of the DC/OS Identity and Access Manager (Bouncer) component, using out-of-band verficiation via public key cryptography.

**NOTE**: In DC/OS Open Source Admin Router is the only authenticator in the system.

DC/OS uses JSON Web Tokens (JWT) for the purpose of authenticating HTTP requests against the cluster. DC/OS authentication tokens are sent via HTTP in the `Authorization` header. The `Authorization` header value must be in the format: `token=<token>`. Other formats like `Bearer <token>` are not supported.

From the [DC/OS CLI](/1.13/cli), you can log in to your cluster which results in obtaining a DC/OS authentication token. The token will then be used for authenticating the logged in on subsequent DC/OS CLI commands. 

## <a name="log-in-cli"></a>Authenticating through DC/OS CLI

Authentication is only supported for DC/OS CLI version 0.4.3 and later. See [here](/1.13/cli/update/) for upgrade instructions.

The DC/OS CLI stores the token in a configuration file in the `.dcos` directory under the home directory of the user running the CLI. This token can be used with the `curl` command to access DC/OS APIs, using `curl` or `wget`. For example, `curl -H 'Authorization: token=<token>' http://cluster`.


## Disabling DC/OS Authentication

If you are doing an [advanced installation](/1.13/installing/production/deploying-dcos/installation/), you can disable authentication by adding this parameter to your configuration file (`genconf/config.yaml`). 

```yaml
oauth_enabled: 'false'
```
For more information, see the configuration [documentation](/1.13/installing/production/advanced-configuration/configuration-reference/).

If you are doing a cloud installation on [AWS](/1.13/installing/oss/cloud/aws/), you can set the `OAuthEnabled` option to `false` on the **Specify Details** step to disable authentication.

If you are doing a cloud installation on [Azure](/1.13/installing/evaluation/azure/), you cannot disable authentication.

Note that if you have already installed your cluster and would like to disable this in-place, you can go through an upgrade with the configuration parameter set.


## Further reading

- [Let’s encrypt DC/OS!](https://mesosphere.com/blog/2016/04/06/lets-encrypt-dcos/):
  a blog post about using [Let's Encrypt](https://letsencrypt.org/) with
  services running on DC/OS.

## Future work

We are looking forward to working with the DC/OS community on improving existing
security features as well as on introducing new ones in the coming releases.

## Next Steps

- [Understand DC/OS security](/1.13/administering-clusters/)
- [Learn how to monitor a DC/OS cluster](/1.13/monitoring/)
