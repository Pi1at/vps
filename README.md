# Nodemaster

Based on the **Nodemaster** scripts is a collection of utilities to manage, setup and update masternode instances.

## Installation

SSH to your VPS and clone the Github repository:

```bash
git clone https://github.com/masternodes/vps.git && cd vps
```

Install & configure your desired master node with options:

```bash
./install.sh -p pivx
```

## Examples for typical script invocation

These are only a couple of examples for typical setups. Check my [easy step-by-step guide for [vultr](/docs/masternode_vps.md) that will guide you through the hardest parts.

**Install & configure 4 PIVX masternodes:**

```bash
./install.sh -p pivx -c 4
```

**Update daemon of previously installed PIVX masternodes:**

```bash
./install.sh -p pivx -u
```

**Install 6 PIVX masternodes with the git release tag "tags/v3.0.5.1"**

```bash
./install.sh -p pivx -c 6 -r "tags/v3.0.5.1"
```

**Wipe all PIVX masternode data:**

```bash
./install.sh -p pivx -w
```

**Install 2 PIVX masternodes and configure sentinel monitoring:**

```bash
./install.sh -p pivx -c 2 -s
```

## Options

The _install.sh_ script support the following parameters:

| Long Option  | Short Option | Values              | description                                                         |
| :----------- | :----------- | ------------------- | ------------------------------------------------------------------- |
| --project    | -p           | project, e.g. "pix" | shortname for the project                                           |
| --net        | -n           | "4" / "6"           | ip type for masternode. (ipv)6 is default                           |
| --release    | -r           | e.g. "tags/v3.0.4"  | a specific git tag/branch, defaults to latest tested                |
| --count      | -c           | number              | amount of masternodes to be configured                              |
| --update     | -u           | --                  | update specified masternode daemon, combine with -p flag            |
| --sentinel   | -s           | --                  | install and configure sentinel for node monitoring                  |
| --wipe       | -w           | --                  | uninstall & wipe all related master node data, combine with -p flag |
| --help       | -h           | --                  | print help info                                                     |
| --startnodes | -x           | --                  | starts masternode(s) after installation                             |

## Troubleshooting the masternode on the VPS

If you want to check the status of your masternode, the best way is currently running the cli e.g. for $MUE via

```
/usr/local/bin/mue-cli -conf=/etc/masternodes/mue_n1.conf getinfo

{
  "version": 1000302,
  "protocolversion": 70701,
  "walletversion": 61000,
  "balance": 0.00000000,
  "privatesend_balance": 0.00000000,
  "blocks": 209481,
  "timeoffset": 0,
  "connections": 5,
  "proxy": "",
  "difficulty": 42882.54964804553,
  "testnet": false,
  "keypoololdest": 1511380627,
  "keypoolsize": 1001,
  "paytxfee": 0.00000000,
  "relayfee": 0.00010000,
  "errors": ""
}
```

# Help, Issues and Questions

I activated the "[issues](https://github.com/masternodes/vps/issues)" option on github to give you a way to document defects and feature wishes. Feel free top [open issues](https://github.com/masternodes/vps/issues) for problems / features you are missing here: [https://github.com/masternodes/vps/issues](https://github.com/masternodes/vps/issues).

I might not be able to reply immediately, but i do usually within a couple of days at worst. I will also happily take any pull requests that make masternode installations easier for everyone ;-)

If this script helped you in any way, please contribute some feedback. BTC donations also welcome and never forget:

**Have fun, this is crypto after all!**

```
BTC  33ENWZ9RCYBG7nv6ac8KxBUSuQX64Hx3x3
```

## Management script (not yet implemented)

The management script release will follow within the next couple of days.

| command                               | description                                  |
| :------------------------------------ | -------------------------------------------- |
| nodemaster start pivx (all\|number)   | start all or a specific pivx masternode(s)   |
| nodemaster restart pivx (all\|number) | stop all or a specific pivx masternode(s)    |
| nodemaster stop pivx (all\|number)    | restart all or a specific pivx masternode(s) |
| nodemaster cleanup pivx (all\|number) | delete chain data for all pivx masternodes   |
| nodemaster status pivx (all\|number)  | systemd process status for a pivx masternode |
| nodemaster tail pivx (all\|number)    | tail debug logs for a pivx masternode        |

# Todo

* provide my Dockerfile & Vagrantfile
* write more test cases
* implement a binary option (?)
* output all supported cryptos as list within help

# Errors

* currently not fully idempotent
