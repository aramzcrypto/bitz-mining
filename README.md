# Mining BITZ on Eclipse via CLI

<div align="center">
  <img src="https://nu.fi/blog/experimental-eclipse-blockchain-support" alt="Eclipse Logo" width="150"/>
  <h3>Complete Guide to Mining $BITZ Tokens via ePOW</h3>
</div>

This repository contains a step-by-step guide for setting up and mining BITZ tokens using the Eclipse Proof of Work (ePOW) system.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Wallet Setup](#wallet-setup)
- [Mining Configuration](#mining-configuration)
- [Starting the Miner](#starting-the-miner)
- [Managing Your BITZ](#managing-your-bitz)
- [Troubleshooting](#troubleshooting)
- [Optimization Tips](#optimization-tips)

## Prerequisites
- Ubuntu Linux system (20.04 LTS or newer)
- Root access or sudo privileges
- Internet connection
- A minimum of 0.005 ETH on Eclipse network

## Installation

### Step 1: Install Rust
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Follow the prompts (select option 1 for default installation). Once installed, load Rust into your current shell:

```bash
source $HOME/.cargo/env
```

### Step 2: Install Required Dependencies
```bash
sudo apt update
sudo apt install -y build-essential pkg-config libssl-dev clang
```

If you encounter Python apt_pkg errors during the update:
```bash
sudo apt-get update --fix-missing
sudo apt-get install --reinstall python3-apt
```

### Step 3: Install Solana CLI
```bash
sh -c "$(curl -sSfL https://release.solana.com/v1.18.2/install)"
```

After installation, update your PATH:
```bash
export PATH="$HOME/.local/share/solana/install/active_release/bin:$PATH"
echo 'export PATH="$HOME/.local/share/solana/install/active_release/bin:$PATH"' >> ~/.bashrc
```

Verify installation:
```bash
solana --version
```

## Wallet Setup

### Step 4: Create a Solana Wallet
```bash
solana-keygen new --no-passphrase
```

This creates a keypair at `~/.config/solana/id.json` and displays your public key and seed phrase.

> ⚠️ **IMPORTANT**: Save your public key and seed phrase securely!

### Step 5: Get Your Private Key
View your private key (for importing to wallets):
```bash
cat ~/.config/solana/id.json
```
This will display an array of numbers - that's your private key. Example output:
```
[12,34,127,170,169,68,18,209,1,87,132,123,118,103,228,238,175,146,218,207,95,58,109,31,204,164,242,54,180,181,120,217,145,214,28,86,130,141,119,250,19,132,8,47,99,221,130,215,106,235,10,98,147,156,254,234,78,233,72,172,46,202,133,144]
```

### Step 6: Install BITZ CLI
```bash
cargo install bitz
```

### Step 7: Configure Solana for Eclipse
```bash
solana config set --url https://mainnetbeta-rpc.eclipse.xyz/
```

### Step 8: Fund Your Eclipse Wallet
Before mining, you need at least 0.005 ETH on Eclipse network.

Get your public key:
```bash
solana address
```

Transfer at least 0.005 ETH to this address on the Eclipse network. You can use a bridge service to move ETH from Ethereum mainnet to Eclipse, or purchase directly from a supporting exchange.

## Mining Configuration

Before starting the mining process, you can configure how many CPU cores to use:

```bash
# Set the number of cores based on your system (example uses 8 cores)
bitz collect --cores 8
```

For optimal performance, leave 1-2 cores free for system operations.

## Starting the Miner

### Step 9: Start Mining in a Screen Session
[Screen](https://www.gnu.org/software/screen/) allows the mining process to continue even if you disconnect from your terminal:

```bash
screen -S eclipse
```

### Step 10: Begin Mining BITZ
```bash
bitz collect
```

**Managing your screen session:**
- To detach from the screen session (keep mining in background):
  - Press `Ctrl+A` then `D`
- To reattach to the session later:
  ```bash
  screen -r eclipse
  ```
- To terminate the mining session:
  - Reattach to the screen, then press `Ctrl+C`

## Managing Your BITZ

Once mining is active, you can manage your BITZ tokens with these commands:

### Check Your Balance
```bash
bitz account
```

### Claim Your Mined Tokens
```bash
bitz claim
```

### View All Available Commands
```bash
bitz -h
```

## Wallet Integration

### Importing to Backpack Wallet

1. Copy your private key array from:
   ```bash
   cat ~/.config/solana/id.json
   ```

2. In Backpack wallet:
   - Go to Settings > Wallets
   - Select "Import wallet"
   - Choose "Import private key"
   - Paste the array of numbers from your Solana keypair

## Troubleshooting

### Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| Command Not Found Errors | Reinstall Python packages: `sudo apt-get install --reinstall python3-apt` |
| Mining Not Starting | Check ETH balance (min 0.005 ETH required) |
| `solana-keygen` Not Found | Verify PATH settings: `echo $PATH` and ensure Solana binaries are included |
| Connection Issues | Verify Eclipse RPC endpoint: `solana config get` |
| Low Mining Rate | Check CPU usage, network connection, and consider adjusting cores |

### Verifying Eclipse RPC Connection
```bash
solana config get
```
The URL should be set to `https://mainnetbeta-rpc.eclipse.xyz/`

## Optimization Tips

- **System Resources**: Allocate appropriate CPU cores with the `--cores` flag
- **Uptime**: Use `screen` or `tmux` to maintain mining sessions during disconnections
- **Monitoring**: Set up basic system monitoring to track performance
- **Thermal Management**: Ensure proper cooling for extended mining sessions
- **Automation**: Consider setting up auto-claim scripts for collected BITZ
- **Security**: Regularly backup your keypair and seed phrase

## Contributing

Contributions to this guide are welcome! Please submit a pull request or open an issue to suggest improvements.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

<div align="center">
  <p>Happy mining! 🚀</p>
  <p>If this guide helped you, consider starring the repository ⭐</p>
</div>
