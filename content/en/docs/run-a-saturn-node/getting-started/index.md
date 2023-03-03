---
title: "Get Started"
description: ""
lead: ""
draft: false
images: []
type: docs
menu:
  docs:
    parent: "lorem"
    identifier: "run-saturn-1-0f678f8604f88f2f645fb62049d718f7"
weight: 200
toc: true
---

## Set up a node

<sub>If you want to switch your node from test net to main net, or vice versa, see [Switch networks](#switch-networks-between-test-net-and-main-net) below.</sub>

1. Install

   - Docker: [instructions here](https://docs.docker.com/engine/install/#server)
   - Docker compose v2: [instructions here](https://docs.docker.com/compose/install/linux/)

2. Change directory to `$SATURN_HOME` (default: `$HOME`) to download the required files

   ```bash
   cd ${SATURN_HOME:-$HOME}
   ```

3. Download the `.env` file

   Note: the `.env` file [does not take precedence](https://docs.docker.com/compose/envvars-precedence/) over env variables set locally.

   - Set the mandatory `FIL_WALLET_ADDRESS` and `NODE_OPERATOR_EMAIL` environment variables in the `.env` file.
   - Set the `SATURN_NETWORK` environment variable in the `.env` file.
     - To join Saturn's Main network and earn FIL rewards, make sure to set `SATURN_NETWORK` to `main`.
     - To join Saturn's Test network, which doesn't earn FIL rewards, set `SATURN_NETWORK` to `test`. Note that this is the default value!
   - By default, the Saturn volume is mounted from `$HOME`. It can be changed by setting the `$SATURN_HOME` environment variable.

   ```bash
   curl -s https://raw.githubusercontent.com/filecoin-saturn/L1-node/main/.env -o .env
   ```

   You can use the text editor of your choice (e.g. `nano` or `vim` on Linux)

4. Download the docker-compose file

   ```bash
   curl -s https://raw.githubusercontent.com/filecoin-saturn/L1-node/main/docker-compose.yml -o docker-compose.yml
   ```

5. Launch it:

   ```bash
   sudo docker compose up -d
   ```

6. Check logs with `docker logs -f saturn-node`
7. Check there are no errors, registration will happen automatically and node will restart once it receives its TLS certificate

In most instances speedtest does a good job of picking "close" servers but for small networks it may be incorrect.
If the speedtest value reported by speedtest seems low, you may want to configure SPEEDTEST_SERVER_CONFIG to point to a different public speedtest server. You will need to install [speedtest CLI](https://www.speedtest.net/apps/cli) in the host and fetch close servers' IDs by doing `speedtest --servers`, then setting `SPEEDTEST_SERVER_CONFIG="--server-id=XXXXX"`

## Switch networks between test net and main net

If you want to switch your node from Saturn's test network (aka `test`) to Saturn's main network (aka `main`), or vice versa, follow these steps:

1. Gracefully halt your node as explained in [Stopping a node](#stopping-a-node).
2. Set the network environment variable `SATURN_NETWORK` to `main`, or `test`, in your `$SATURN_HOME/.env` file (default: `$HOME/.env`).
3. Delete contents in `$SATURN_HOME/shared/ssl` (default: `$HOME/shared/ssl`).
4. Start the node again with `docker compose -f $SATURN_HOME/docker-compose.yml up -d`.
5. Check logs with `docker logs -f saturn-node`

### Obtaining a Filecoin wallet address

You need to own a Filecoin wallet to receive FIL payments.

- [Official Filecoin wallet documentation](https://docs.filecoin.io/get-started/overview/#wallets)

- If you have an account on a Centralized Exchange (Coinbase, Binance, etc.) that supports Filecoin,
  go through the steps to deposit Filecoin and you'll be given an wallet address. This is recommended
  if you don't want to manage your wallet's seed phrase.

- Web wallets
  - [Filfox wallet](https://wallet.filfox.info/)
  - [Glif](https://wallet.glif.io/) - Supports Ledger
- Desktop wallets
  - [Exodus](https://www.exodus.com/)
- Mobile wallets
  - [FoxWallet](https://foxwallet.com/)

⚠️ Please follow crypto wallet best practices. Never share your seed phrase with anyone or enter it into websites.
The Saturn team will **never** DM you or ask you to verify/validate/upgrade your wallet. If you need assistance,
please ask in public channels such as the [#filecoin-saturn](https://filecoinproject.slack.com/archives/C03DH0BL02E)
Slack.

### Receiving FIL payments

When payments are scheduled to be sent out, your Filecoin wallet will receive a FIL payment.

### Node monitoring

- https://dashboard.strn.network - View historical data on your bandwidth contributions, FIL earnings, and more.
- https://orchestrator.strn.pl/stats - View detailed, real-time stats on every Saturn node.

