# 📘 PolkadotGovChain

**A Governance-Enabled Substrate Parachain on Polkadot**

<p align="center">
  <a href="https://opensource.org/licenses/Apache-2.0"><img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg" alt="License"></a>
  <a href="https://github.com/paritytech/polkadot-sdk"><img src="https://img.shields.io/badge/Substrate-v7.0.1-brightgreen" alt="Substrate"></a>
  <a href="https://github.com/paritytech/polkadot-sdk"><img src="https://img.shields.io/badge/Polkadot-SDK-e6007a" alt="Polkadot SDK"></a>
</p>

PolkadotGovChain is a custom **Substrate-based parachain** built using the [Polkadot SDK](https://github.com/paritytech/polkadot-sdk). It provides a production-ready governance environment featuring on-chain democracy, council governance, asset management, and cross-chain messaging (XCM) compatibility.

This project serves as:
- 🎓 A **learning reference** for building governance-enabled parachains
- 🏆 A **hackathon-ready** Polkadot parachain template
- 🏛️ A **foundation** for DAO and community-chain experiments
- 🧪 A **Web3 governance research** platform

---

## ✨ Features

| Feature | Pallet | Status |
|---------|--------|--------|
| **Native Token Management** | `pallet_balances` | ✅ |
| **Custom Asset Issuance** | `pallet_assets` | ✅ |
| **Council Governance** | `pallet_collective` | ✅ |
| **Public Democracy** | `pallet_democracy` | ✅ |
| **Scheduled Executions** | `pallet_scheduler` | ✅ |
| **Proposal Storage** | `pallet_preimage` | ✅ |
| **Admin Control** | `pallet_sudo` | ✅ |
| **Cross-Chain Messaging** | `pallet_xcm` + `parachain_system` | ✅ |
| **Parachain Collator** | Built-in | ✅ |

### Core Capabilities
- ✅ **On-chain Democracy** — Public proposals and referendum voting
- ✅ **Council Governance** — Elected council for fast-track proposal execution
- ✅ **Asset Management** — Create and manage custom fungible tokens
- ✅ **Scheduled Calls** — Time-delayed transaction execution
- ✅ **XCM Ready** — Cross-chain messaging support for Polkadot ecosystem
- ✅ **Collator Node** — Produces blocks connected to relay chain

---

## 🏗️ Architecture

```
Polkadot Relay Chain (Rococo / Local Testnet)
        │
        ├── Validator: Alice
        ├── Validator: Bob
        │
        └─── PolkadotGovChain Parachain (ParaId: 1000)
              │
              ├── Governance Layer
              │   ├── pallet_democracy (Public Proposals)
              │   ├── pallet_collective (Council)
              │   └── pallet_scheduler (Delayed Execution)
              │
              ├── Economic Layer
              │   ├── pallet_balances (Native Token)
              │   └── pallet_assets (Custom Tokens)
              │
              └── Communication Layer
                  ├── pallet_xcm (Cross-chain Messages)
                  └── pallet_xcmp_queue (Message Queue)
```

---

## 🚀 Quick Start

### Prerequisites
- Rust toolchain (1.84+)
- Cargo
- Git
- Zombienet (for local testing)

### 1. Clone & Build

```bash
# Clone the repository
git clone https://github.com/codewithdubeyji/PolkadotGovChain.git
cd PolkadotGovChain

# Build the parachain node
cargo build --release
```

**Build time:** ~7-10 minutes  
**Binary location:** `./target/release/parachain-template-node`

### 2. Generate Genesis Files

```bash
# Export WASM runtime
./target/release/parachain-template-node export-genesis-wasm --chain local > para-2000-wasm

# Export genesis state
./target/release/parachain-template-node export-genesis-state --chain local > para-2000-genesis
```

### 3. Run Local Network with Zombienet

```bash
# Install Zombienet (if not already installed)
curl -LO https://github.com/paritytech/zombienet/releases/download/v1.3.116/zombienet-linux-x64
chmod +x zombienet-linux-x64
sudo mv zombienet-linux-x64 /usr/local/bin/zombienet

# Build Polkadot relay chain binary (if not already built)
cd /path/to/polkadot-sdk
cargo build --release -p polkadot

# Spawn the network
cd templates/parachain
zombienet -p native spawn zombienet.toml
```

---

## 🌐 Connect to UI

| Network | RPC Port | Polkadot.js Apps URL |
|---------|----------|----------------------|
| **Relay Chain** (Rococo Local) | 9944 | [Connect to Relay](https://polkadot.js.org/apps/?rpc=ws://127.0.0.1:9944) |
| **Parachain** (PolkadotGovChain) | 9988 | [Connect to Parachain](https://polkadot.js.org/apps/?rpc=ws://127.0.0.1:9988) |

### Network Topology
- **Alice** — Relay chain validator (Port: 9944)
- **Bob** — Relay chain validator (Port: 9955)
- **Charlie** — Parachain collator (Port: 9988)

---

## 🧩 Runtime Pallets

### Governance Stack
| Pallet | Description | Key Functions |
|--------|-------------|---------------|
| `pallet_democracy` | Public proposals & referendums | `propose()`, `vote()`, `second()` |
| `pallet_collective` | Council governance (fast-track) | `propose()`, `vote()`, `execute()` |
| `pallet_scheduler` | Scheduled on-chain calls | `schedule()`, `cancel()` |
| `pallet_preimage` | Store proposal preimages | `notePreimage()` |

### Economic Stack
| Pallet | Description | Key Functions |
|--------|-------------|---------------|
| `pallet_balances` | Native token (UNIT) | `transfer()`, `transfer_keep_alive()` |
| `pallet_assets` | Custom fungible tokens | `create()`, `mint()`, `transfer()` |

### Infrastructure Stack
| Pallet | Description | Key Functions |
|--------|-------------|---------------|
| `pallet_sudo` | Superuser control | `sudo()`, `set_key()` |
| `pallet_xcm` | Cross-chain messaging | `send()`, `execute()` |
| `pallet_xcmp_queue` | XCM message queue | Auto-managed |
| `pallet_parachain_system` | Parachain interface | Auto-managed |

---

## 🎯 Use Cases

### 1. **DAO Governance Chains**
Build decentralized autonomous organizations with on-chain voting and proposal execution.

### 2. **Community Token Platforms**
Issue and manage community tokens with built-in governance mechanisms.

### 3. **Cross-Chain Governance**
Experiment with multi-chain governance using XCM messaging.

### 4. **Voting Systems**
Implement referendum-based voting for decentralized decision-making.

### 5. **Web3 Learning & Research**
Study Polkadot parachain architecture and Substrate runtime development.

---

## 📚 Testing Guide

### Test 1: Create & Mint Assets

1. Connect to parachain at `ws://127.0.0.1:9988`
2. Go to **Developer → Extrinsics**
3. Select **ALICE** account
4. Extrinsic: `assets → create`
   - `id`: `1`
   - `admin`: ALICE
   - `minBalance`: `1`
5. Submit transaction
6. Mint tokens: `assets → mint`
   - `id`: `1`
   - `beneficiary`: ALICE
   - `amount`: `1000000`

### Test 2: Council Proposal

1. **Developer → Extrinsics** → ALICE
2. Extrinsic: `council → propose`
   - `threshold`: `1`
   - `proposal`: `system.remark("Test proposal")`
   - `lengthBound`: `100`
3. Go to **Governance → Council → Motions**
4. Vote: `council → vote`

### Test 3: Democracy Referendum

1. **Developer → Extrinsics** → ALICE
2. Create preimage: `preimage → notePreimage`
   - `encodedProposal`: `system.remark("Democracy test")`
3. Submit proposal: `democracy → propose`
   - `proposal`: (preimage hash)
   - `value`: `100000000000`
4. Check **Governance → Democracy**

---

## 🛠️ Development Status

| Component | Status | Notes |
|-----------|--------|-------|
| Relay chain connection | ✅ Complete | Tested with Rococo Local |
| Parachain collator | ✅ Complete | Charlie node operational |
| Governance pallets | ✅ Integrated | Council + Democracy working |
| Assets pallet | ✅ Integrated | Token creation tested |
| XCM base wiring | ✅ Ready | Message passing enabled |
| Genesis configuration | ✅ Complete | Alice in council |
| Zombienet setup | ✅ Complete | Auto-spawns network |
| HRMP channels | ⚠️ Future work | Optional for production |

---

## 📖 Resources & Credits

This project is built using open-source software from the Polkadot and Substrate ecosystem:

### Acknowledgements
- **[Polkadot SDK](https://github.com/paritytech/polkadot-sdk)** — Substrate framework and Polkadot runtime
- **[Substrate](https://github.com/paritytech/substrate)** — Blockchain framework (now part of Polkadot SDK)
- **[Zombienet](https://github.com/paritytech/zombienet)** — Local network testing tool
- **[Polkadot-JS Apps](https://github.com/polkadot-js/apps)** — Universal Substrate UI
- **[Parity Technologies](https://www.parity.io/)** — Core developers of Polkadot & Substrate
- **Polkadot Community** — Documentation, tutorials, and ecosystem support
- **Substrate Builders Program** — Technical guidance and resources

### Documentation References
- [Polkadot Wiki](https://wiki.polkadot.network/)
- [Substrate Documentation](https://docs.substrate.io/)
- [Polkadot SDK Docs](https://paritytech.github.io/polkadot-sdk/)
- [Cumulus Documentation](https://github.com/paritytech/cumulus)

**All credits go to the Polkadot and Substrate open-source community.**

---

**PolkadotGovChain Contributors**

Built as a governance-enabled parachain project using Polkadot SDK.

For questions, issues, or contributions:
- Open an issue on GitHub
- Submit a pull request
- Join the [Polkadot Discord](https://dot.li/discord)

---

## 🔗 Project Links

- **GitHub Repository:** [[YOUR_GITHUB_URL](https://github.com/codewithdubeyji/PolkadotGovChain.git)]
- **Polkadot.js Connect:** [ws://127.0.0.1:9988](https://polkadot.js.org/apps/?rpc=ws://127.0.0.1:9988)
