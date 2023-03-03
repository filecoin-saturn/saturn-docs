---
title: "Switch Networks"
description: ""
lead: ""
draft: false
images: []
type: docs
menu:
  docs:
    parent: "lorem"
    identifier: "switch-0f678f8604f88f2f645fb62049d718f7"
weight: 400
toc: true
---

## Switch networks between test net and main net

If you want to switch your node from Saturn's test network (aka `test`) to Saturn's main network (aka `main`), or vice versa, follow these steps:

1. Gracefully halt your node as explained in [Stopping a node](#stopping-a-node).
2. Set the network environment variable `SATURN_NETWORK` to `main`, or `test`, in your `$SATURN_HOME/.env` file (default: `$HOME/.env`).
3. Delete contents in `$SATURN_HOME/shared/ssl` (default: `$HOME/shared/ssl`).
4. Start the node again with `docker compose -f $SATURN_HOME/docker-compose.yml up -d`.
5. Check logs with `docker logs -f saturn-node`

