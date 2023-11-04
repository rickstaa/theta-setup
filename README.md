# Theta Edge Node Setup Guide

Welcome to the heart of my Theta edge node setup! This repository houses the docker-compose file that fuels my edge node.

## System Snapshot

### Key Components

- **Operating System:** [Ubuntu 22.04](https://releases.ubuntu.com/jammy/) (Kernel version: 5.15.0-86-generic).
- **Graphics Processing Unit (GPU):** 1x [NVIDIA GeForce GTX 1070 Ti](https://www.nvidia.com/en-us/geforce/news/nvidia-geforce-gtx-1070-ti/).
- **Power Supply Unit (PSU):** [Corsair HX1200i](https://www.corsair.com/us/en/p/psu/cp-9020070-na/hxi-series-hx1200i-high-performance-atx-power-supply-1200-watt-80-plus-platinum-certified-psu-cp-9020070-na) PSU.

## How to Use

### Prerequisites

- Ensure [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/) are installed on your system.

### Setup

1. Clone this repository.
2. Introduce a `.theta_password.txt` file to this directory and input your Theta wallet password.
3. Guarantee that the root user is the file owner:

   ```bash
   sudo chown root:root .theta_password.txt
   ```

4. Confirm the file has the correct permissions:

   ```bash
   sudo chmod 600 .theta_password.txt
   ```

5. Initiate the Theta edge node using Docker Compose:

   ```bash
   sudo docker compose up -d
   ```

6. Confirm the edge node is operational by executing `docker ps`.

Your edge node is now primed to receive jobs from the Theta network.

> \[!WARNING]
> Ensure root access for running Docker containers on your system. If you've previously followed [this guide](https://docs.docker.com/engine/install/linux-postinstall/) for non-root users, revert those steps. Failure to do so may expose your wallet password.

### Get Node Info

As outlined in the [Theta docs](https://docs.thetatoken.org/docs/theta-edge-node), fetch your node's info by executing:

```bash
curl -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"edgecore.GetEdgeNodeSummary","params":[],"id":1}' http://localhost:17888/rpc
```

Though the edgcore endpoints are not yet published in the [rpc-api-reference](https://docs.thetatoken.org/docs/rpc-api-reference#getaccount), the following methods were discovered in the Theta discord:

- `edgecore.GetEdgeNodeSummary`
- `edgecore.GetVersion`
- `edgecore.GetStatus`
- `edgecore.GetPeers`

### Interact With The Theta Wallet

You can interact with the Theta wallet by importing the keystore file found in the `~/.edgelauncher/edgecore/key/encrypted` folder into the [Theta Wallet web app](https://wallet.thetatoken.org/).
