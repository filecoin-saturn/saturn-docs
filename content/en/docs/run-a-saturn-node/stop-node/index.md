---
title: "Stop Your Node"
description: ""
lead: ""
draft: false
images: []
type: docs
menu:
  docs:
    parent: "lorem"
    identifier: "stop-0f678f8604f88f2f645fb62049d718f7"
weight: 400
toc: true
---

## Stopping a node

To gracefully stop a node and not receive a penalty, run:

```bash
  sudo docker stop --time 1800 saturn-node
```

or if you are in your `$SATURN_HOME` folder with the Saturn `docker-compose.yml` file:

```bash
  sudo docker compose down
```

We are setting the `stop_signal` and the `stop_grace_period` in our Docker compose file to avoid issues.
If you have a custom setup, make sure to send a SIGTERM to your node and wait at least 30 minutes for it to drain.

