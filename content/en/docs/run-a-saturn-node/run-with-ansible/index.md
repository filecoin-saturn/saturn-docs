---
title: "Run With Ansible"
description: ""
lead: ""
draft: false
images: []
type: docs
menu:
  docs:
    parent: "lorem"
    identifier: "run-ansible-0f678f8604f88f2f645fb62049d718f7"
weight: 500
toc: true
---

## Set up a node with [Ansible](https://docs.ansible.com/ansible/latest/index.html)

From [here](https://docs.ansible.com/ansible/latest/index.html#about-ansible):

> "Ansible is an IT automation tool. It can configure systems, deploy software, and orchestrate more advanced IT tasks such as continuous deployments or zero downtime rolling updates."

This playbook is meant as a bare-bones approach to set up an L1. It simply automates running the steps described [above](#set-up-a-node). A consequence of this is that when run it will restart a crashed L1 node docker container.
It also presents a basic approach to server hardening which is by no means thorough.

**Note: The security of your servers is your responsibility. You should do your own research to ensure your server follows security best practices.**

If you're looking for a playbook which covers server hardening, monitoring and logging please check out https://github.com/hyphacoop/ansible-saturn-l1.

Currently, this playbook runs on the following Linux distros:

- Ubuntu
- Debian
- CentOS

These instructions are to be run in a machine with [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) >= 2.14 installed.
This machine is known as your control node and it should not be the one to run your L1 node.

Most commands are run as root and your ssh user should have root access on the target machine.

1. Install the required Ansible modules

```
ansible-galaxy collection install community.docker
```

2. Clone this repository and `cd` into it.

3. For target host connectivity, ssh keys are recommended and this playbook can help you with that.

   Note: Using the playbook for this is completely optional.

   1. Make sure you have configured `ansible_user` and `ansible_ssh_pass` for your target host in your inventory file. See more [here](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#adding-variables-to-inventory).
   1. Setup an `authorized_keys` file with your public ssh keys in the cloned repository root.
   1. Run `ansible-playbook -i <path_to_your_inventory> -l <host_label> --skip-tags=config,harden,run playbooks/l1.yaml`

4. Ensure your control node has ssh access to your target machine(s).

- Make sure to specify which hosts you want to provision in your inventory file.

```bash
ansible -vvv -i <path_to_your_inventory> <host_label> -m ping
```

5. Replace the environment varariable values where appropriate and export them.

- If **Main network:** Set `SATURN_NETWORK` to `main`
- If you are switching networks check [Switching networks](#switching-networks) and rerun step 4 and 5.
- You can define a host-specific `SATURN_HOME` by setting a `saturn_root` variable for that host on your inventory file. See more [here](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#adding-variables-to-inventory).

```bash
export FIL_WALLET_ADDRESS=<your_fil_wallet_address>; export NODE_OPERATOR_EMAIL=<your_email>; export SATURN_NETWORK=test
```

6. Run the playbook

- Feel free to use host labels to filter them or to deploy incrementally.
- We're skipping the bootstrap play by default, as it deals with setting authorized ssh keys on the target machine. See 2 for more info.

```bash
ansible-playbook -i <path_to_your_inventory> -l <host_label> --skip-tags=bootstrap playbooks/l1.yaml
```

- To skip the hardening step run this instead:

```bash
ansible-playbook -i <path_to_your_inventory> -l <host_label> --skip-tags=bootstrap,harden playbooks/l1.yaml
```
