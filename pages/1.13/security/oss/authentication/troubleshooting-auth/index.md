---
layout: layout.pug
navigationTitle: Troubleshooting authentication
title: Troubleshooting authentication
excerpt: Troubleshooting authentication issues in Open DC/OS

menuWeight: 30
---
## Ad Blockers and the DC/OS UI

During testing, we have observed issues with loading the DC/OS UI login page when certain ad blockers such as HTTP Switchboard or Privacy Badger are active. Other ad blockers like uBlock Origin are known to work.

## Debugging

### Login

The IAM is the only entity emitting DC/OS authentication tokens.
To debug login problems, check the IAM (Bouncer) on the masters using the following commands.

```bash
sudo journalctl -u dcos-bouncer.service
```

### Authentication

Admin Router is the only entity verfiying DC/OS authentication tokens.
To debug authentication problems, check the Admin Router on the masters using the following commands.

```bash
sudo journalctl -u dcos-adminrouter.service
```

