---
layout: layout.pug
navigationTitle: External user accounts
title: Managing external user accounts
excerpt: Managing external user accounts
menuWeight: 10
---
<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

An external user is automatically created for the first user who logs in to the DC/OS cluster via a single sign-on flow through Auth0.

# Add external users from the web interface

1.  Log in to the web interface with your username (Google, GitHub, and Microsoft) and password.

2.  Click on  **Organization** in the left hand menu. From the **Users** screen, click the plus sign (**+**) in the upper right corner, and fill in the new user email address. New users are automatically sent an email notifying them of access to DC/OS.

![new DC/OS user](/1.13/img/1-11-add-user-to-cluster.png)

Figure 1. Adding a new user

# Add external users from the CLI
You can add external users to your DC/OS cluster from a terminal by using the `dcos_add_user.py` script. This script is included by default with your DC/OS installation.

**Prerequisites:**

- DC/OS is [installed](/1.13/installing/)

1.  [SSH](/1.13/administering-clusters/sshcluster/) to a master node and run this command, where `<email>` is the user's email:

    ```bash
    sudo -i dcos-shell /opt/mesosphere/bin/dcos_add_user.py <email>
    ```

2.  Send the URL of your DC/OS cluster (e.g. `http://<public-master-ip>/`) to the new user. The user specified by `<email>` can now login and access the cluster.

# Delete users
1.  From the **Users** screen, select the user name and click **Delete**.
2.  Click **Delete** to confirm the action.

<img src="/1.12/img/1-11-delete-user.png" alt="delete-user" width="350" height="300" border="2">

 Figure 2. Deleting a user
