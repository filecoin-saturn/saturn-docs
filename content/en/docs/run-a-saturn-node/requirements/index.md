---
title: "Requirements"
description: ""
lead: ""
draft: false
images: []
type: docs
menu:
  docs:
    parent: "lorem"
    identifier: "reqs-0f678f8604f88f2f645fb62049d71943"
weight: 100
toc: true
---

### General requirements

- Filecoin wallet address
- Email address

### Node hardware requirements

- Linux server with a static public IPv4 address
- Root access / passwordless sudo user ([How to](https://askubuntu.com/questions/147241/execute-sudo-without-password))
- Ports 80 and 443 free and public to the internet
- [Docker](https://www.docker.com/) installed ([Instructions here](https://docs.docker.com/engine/install/#server)) with [Docker Compose v2](https://www.docker.com/blog/announcing-compose-v2-general-availability/)
- CPU with 6 cores (12+ cores recommended). [CPU Mark](https://www.cpubenchmark.net/cpu_list.php) of 8,000+ (20,000+ recommended)
- 10Gbps upload link minimum<sup>1</sup> ([Why 10Gbps?](https://github.com/filecoin-saturn/L1-node/blob/main/docs/faq.md#why-is-10-gbps-uplink-required))
- 32GB RAM minimum (128GB+ recommended)
- 2TB SSD storage minimum (16TB+ NVMe recommended)<sup>2</sup>

**Only one node per physical host is allowed. If you want to run multiple nodes, you need to run them on dedicated hardware.<br>
Multi-noding (Sharing CPU, RAM, Uplink or storage among nodes) is not allowed.**

<sub>
<sup>1</sup> The more you can serve &rarr; greater FIL earnings<br>
<sup>2</sup> Bigger disk &rarr; bigger cache &rarr; greater FIL earnings
</sub>



