# Gensyn-Swarm

# Running an RL Swarm (Testnet) Node

**RL Swarm** is an open-source framework developed by **GensynAI** for building distributed reinforcement learning (RL) training networks over the internet.
This guide walks you through setting up an RL Swarm node and a web-based dashboard to monitor swarm activity on the **Gensyn Testnet**.

---

## ⚙️ Hardware Requirements

The latest Gensyn Testnet update trains *reasoning-gym* datasets on the swarm network. Supported default models include:

* `Gensyn/Qwen2.5-0.5B-Instruct`
* `Qwen/Qwen3-0.6B`
* `nvidia/AceInstruct-1.5B`
* `dnotitia/Smoothie-Qwen3-1.7B`
* `Gensyn/Qwen2.5-1.5B-Instruct`

Select a model based on your hardware capacity:

* **Light setups:** Use smaller models like `Qwen2.5-0.5B` or `Qwen3-0.6B`
* **High-end setups:** Use larger models for better training performance

### CPU Requirements

* Architecture: `arm64` or `x86`
* Memory: Minimum **32 GB RAM**

> ⚠️ Running other programs during training may cause crashes.

### GPU Requirements

* Supported GPUs: RTX 3090 / 4090 / 5090 / A100 / H100
* Recommended: ≥ 24GB VRAM (supports GPUs <24GB as well)
* CUDA Driver: ≥ 12.4

This guide follows the easiest default setup method for joining the Testnet. For more details, refer to the **[Official Repository](https://github.com/gensyn-ai/rl-swarm)**.

---

## 📚 Quick Navigation

### 🚀 Getting Started

* Environment Setup (Windows, Cloud GPU, VPS)
* Install Dependencies (Python, Node.js, Yarn, etc.)
* HuggingFace Setup
* Clone Repository

### 🏃 Running Your Node

* Start the Swarm (CLI / Docker)
* Login & Authentication
* Join the Judge (AI Prediction Market)
* Node Naming & Management

### 🔧 Advanced Setup

* Multiple Nodes
* Backup & Recovery
* Node Health & Monitoring
* Telegram Bot Setup

### 🛠 Maintenance

* Update Node
* Troubleshooting Common Issues

### 🌐 Cloud Providers

* Vast.ai
* QuickPod
* Hyperbolic
* VPS (CPU-only)

### 📊 Monitoring & Rewards

* Official Dashboard
* Contract Explorer
* Telegram Notifications

---

## 🧩 Environment Setup

### **Method 1: Windows (Home PC)**

If you’re using Windows, first install **Ubuntu** via WSL.

**Install Ubuntu on Windows:** [Guide Link]

Then verify your NVIDIA Driver and CUDA Toolkit:

```bash
sudo apt-get update
sudo apt-get install -y nvidia-cuda-toolkit
nvidia-smi
nvcc --version
```

---

### **Method 2: Rent a Cloud GPU**

#### 🧠 Option A: Vast.ai

1. Register on [Vast.ai](https://vast.ai)
2. Create or upload your **SSH key**
3. Select the **PyTorch (Vast)** template
4. Choose a GPU (≥24GB VRAM recommended)
5. Increase disk space to **50GB**
6. Top up credits and rent
7. Connect via the provided SSH command
   *(add `-L 3000:localhost:3000` for web dashboard access)*

#### ⚡ Option B: QuickPod (No SSH Key Required)

1. Register and verify your account
2. Deposit cryptocurrency
3. Choose **CUDA 12.4** template
4. Filter and rent GPUs (e.g. RTX 3090/4090)
5. Connect via Web Terminal or SSH command

#### 🔋 Option C: Hyperbolic

1. Sign up on [Hyperbolic Dashboard](https://hyperbolic.xyz)
2. Add your public SSH key in **Settings**
3. Rent a GPU (e.g. RTX 4090, PyTorch template)
4. Connect using SSH with the `-L 3000:localhost:3000` flag

---

### **Method 3: VPS (CPU-only)**

You can also run RL Swarm on a VPS with at least **16 cores and 64GB RAM**.
Recommended providers: [Hostbrr](https://hostbrr.com)

---

## 🧱 Installation Steps

### 1. Install Dependencies

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install screen curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip -y
sudo apt install python3 python3-pip python3-venv python3-dev -y
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo bash -
sudo apt install -y nodejs
npm install -g yarn
curl -o- -L https://yarnpkg.com/install.sh | bash
```

### 2. Setup HuggingFace

* Create a [HuggingFace Account](https://huggingface.co/join)
* Generate an **Access Token** with *write* permissions

### 3. Clone the RL Swarm Repository

```bash
git clone https://github.com/gensyn-ai/rl-swarm/
```

---

## 🏃 Running the Swarm

### **CLI Method (GPU)**

```bash
screen -S swarm
cd rl-swarm
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

### **Docker Method (Mac, CPU, GPU)**

```bash
screen -S swarm
cd rl-swarm
docker compose run --rm --build -Pit swarm-cpu   # For CPU
docker compose run --rm --build -Pit swarm-gpu   # For GPU
```

---

## 🔑 Login Process

After starting, you’ll see:

> “Waiting for userData.json to be created…”

Then open:

* **Local PC:** [http://localhost:3000](http://localhost:3000)
* **Cloud/VPS:** Use LocalTunnel:

```bash
sudo npm install -g localtunnel
lt --port 3000
```

Visit the generated URL and log in to Gensyn.

---

## ⚖️ Join the Judge (Optional)

When prompted:

```
Would you like to participate in the AI Prediction Market? (Y/n)
```

Press **Enter** or **Y** to join.
Your model will engage in a prediction-based reasoning game on the Testnet.

---

## 🦔 Node Identity

Your node’s unique **animal name** will appear in logs (e.g., *whistling hulking armadillo*).
Use `CTRL + SHIFT + F` to search “Hello” in the terminal.

---

## 🧩 Screen Management

| Action   | Command                 |
| -------- | ----------------------- |
| Minimize | `CTRL + A + D`          |
| Reopen   | `screen -r swarm`       |
| Stop     | `screen -XS swarm quit` |

---

## 🔐 Backup & Recovery

Backup your identity file:

```
/root/rl-swarm/swarm.pem
```

This file stores your node credentials.
You can transfer it via SFTP or MobaxTerm to your local system for safekeeping.

To restore:

```bash
put swarm.pem /home/ubuntu/rl-swarm/swarm.pem
```

---

## 📊 Node Monitoring

* **Dashboard:** [Gensyn Testnet](https://dashboard.gensyn.ai)
* **Contract Explorer:** [Alchemy Explorer](https://gensyn-testnet.explorer.alchemy.com)
* **Telegram Bot:** Setup instructions in Gswarm Docs

---

## 🧭 Node Maintenance

### Update Node

```bash
cd rl-swarm
git pull
```

If issues occur, backup `swarm.pem`, delete the repo, reclone it, and restore the file.

### Troubleshooting

Common issues include:

* **CPU config errors** → edit config YAML
* **Daemon timeout** → increase to 120s
* **CUDA memory** → reduce batch size or precision

---

