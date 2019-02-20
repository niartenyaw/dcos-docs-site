---
layout: layout.pug
navigationTitle:  Authentication
excerpt: Handling authentication in DC/OS
title: Authentication
menuWeight: 20
---

<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->


The DC/OS user database is persisted in CockroachDB running on master nodes in the table named `users`. Tokens that are sent to DC/OS in the HTTP `Authorization` header must be in this format: `token=<token>`. Currently the format `Bearer <token>` is not supported.

DC/OS Open Source provides user authentication through Admin Router, which is the only authenticator in the system. Different DC/OS user types can be configured via the [IAM API](/1.13/security/oss/iam-api/); see [User Management](/1.13/security/oss/user-management/). From the [DC/OS CLI](/1.13/cli), you can authenticate to your cluster or even opt out of Auth0-based authentication. 


## <a name="log-in-cli"></a>Authenticating through DC/OS CLI

Authentication is only supported for DC/OS CLI version 0.4.3 and later. See [here](/1.13/cli/update/) for upgrade instructions.

The DC/OS CLI stores the token in a configuration file in the `.dcos` directory under the home directory of the user running the CLI. This token can be used with the `curl` command to access DC/OS APIs, using `curl` or `wget`. For example, `curl -H 'Authorization: token=<token>' http://cluster`.


## Authentication opt-out

If you are doing an [advanced installation](/1.13/installing/production/deploying-dcos/installation/), you can opt out of Auth0-based authentication by adding this parameter to your configuration file (`genconf/config.yaml`). 

```yaml
oauth_enabled: 'false'
```
For more information, see the configuration [documentation](/1.13/installing/production/advanced-configuration/configuration-reference/).

If you are doing a cloud installation on [AWS](/1.13/installing/oss/cloud/aws/), you can set the `OAuthEnabled` option to `false` on the **Specify Details** step to disable authentication.

If you are doing a cloud installation on [Azure](/1.13/installing/evaluation/azure/), you cannot disable authentication. This option will be added in a future releasealong with other options to customize authentication.

Note that if you have already installed your cluster and would like to disable this in-place, you can go through an upgrade with the same parameter set.


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

 [1]: https://en.wikipedia.org/wiki/STARTTLS
