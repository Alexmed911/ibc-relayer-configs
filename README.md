# ⚡ IBC Relayer Configs

> Ready-to-use IBC relayer configurations for the Cosmos ecosystem. Compatible with **Hermes** (Rust) and **Go Relayer**.

[![IBC](https://img.shields.io/badge/IBC-Protocol-6C35DE?style=flat-square)](https://ibcprotocol.org)
[![Hermes](https://img.shields.io/badge/Hermes-Relayer-orange?style=flat-square)](https://hermes.informal.systems)
[![Go Relayer](https://img.shields.io/badge/Go-Relayer-00ADD8?style=flat-square&logo=go)](https://github.com/cosmos/relayer)

## Overview

This repo contains production IBC relayer configurations used in active relaying operations across the Cosmos ecosystem. All channels are verified and actively maintained.

## Channel Index

| Path | Chain A | Chain B | Channel A | Channel B | Status |
|------|---------|---------|-----------|-----------|--------|
| cosmos-osmosis | cosmoshub-4 | osmosis-1 | channel-141 | channel-0 | ✅ Active |
| cosmos-sei | cosmoshub-4 | pacific-1 | channel-562 | channel-0 | ✅ Active |
| cosmos-injective | cosmoshub-4 | injective-1 | channel-220 | channel-1 | ✅ Active |
| cosmos-neutron | cosmoshub-4 | neutron-1 | channel-569 | channel-1 | ✅ Active |
| osmosis-sei | osmosis-1 | pacific-1 | channel-782 | channel-1 | ✅ Active |
| osmosis-injective | osmosis-1 | injective-1 | channel-122 | channel-8 | ✅ Active |
| osmosis-persistence | osmosis-1 | core-1 | channel-6 | channel-6 | ✅ Active |
| osmosis-evmos | osmosis-1 | evmos_9001-2 | channel-204 | channel-0 | ✅ Active |
| sei-injective | pacific-1 | injective-1 | channel-27 | channel-144 | ✅ Active |
| neutron-astroport | neutron-1 | phoenix-1 | channel-25 | channel-229 | ✅ Active |

## Quick Start

### Hermes

```bash
# Install Hermes
cargo install ibc-relayer-cli --bin hermes --locked

# Copy config
cp hermes/config.toml ~/.hermes/config.toml
# Edit with your node RPC endpoints and keys

# Add keys
hermes keys add --chain cosmoshub-4 --mnemonic-file /path/to/mnemonic
hermes keys add --chain osmosis-1 --mnemonic-file /path/to/mnemonic

# Start relaying
hermes start
```

### Go Relayer

```bash
# Install
go install github.com/cosmos/relayer/cmd/rly@latest

# Init
rly config init
cp rly/config.yaml ~/.relayer/config/config.yaml

# Add keys
rly keys restore cosmoshub-4 default "your mnemonic here"
rly keys restore osmosis-1 default "your mnemonic here"

# Start
rly start cosmos-osmosis
```

## Structure

```
ibc-relayer-configs/
├── hermes/
│   ├── config.toml          # Hermes main config
│   └── chains/              # Per-chain configs
├── rly/
│   ├── config.yaml          # Go relayer config
│   └── paths/               # Channel path definitions
├── channels/
│   └── *.json               # Channel metadata
└── scripts/
    ├── start_hermes.sh
    └── check_channels.sh
```

## Tips

- Always run a **full node** for chains you relay — don't use public RPCs for relaying
- Set `memo` in your config to identify your relayer on-chain
- Monitor packet queues with `hermes query packet pending`
- Use `clear_packets` periodically to flush stuck packets

## License

MIT
