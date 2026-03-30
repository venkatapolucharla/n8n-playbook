# n8n Installation & Setup Guide

## Table of Contents

1. [What is n8n?](#what-is-n8n)
2. [Creating an n8n Cloud Account (n8n.io)](#creating-an-n8n-cloud-account)
3. [Installing n8n Locally on macOS](#installing-n8n-locally-on-macos)
4. [Installing n8n Locally on Windows](#installing-n8n-locally-on-windows)
5. [First Launch & Verification](#first-launch--verification)
6. [Troubleshooting Common Issues](#troubleshooting-common-issues)

---

## What is n8n?

n8n (pronounced "n-eight-n") is a free and open-source workflow automation tool. It allows you to connect different services and applications together to automate repetitive tasks without writing code. n8n can be self-hosted on your own infrastructure or used via the cloud-hosted version at **n8n.io**.

**Key Features:**

- Visual workflow builder with a drag-and-drop interface
- 400+ built-in integrations (nodes)
- Self-hosting option for full data control
- Support for custom code (JavaScript/Python) within workflows
- Webhook support for real-time triggers
- Community-driven with an active ecosystem

---

## Creating an n8n Cloud Account (n8n.io)

If you prefer a managed, cloud-hosted version of n8n without local setup, follow these steps:

### Step 1: Visit n8n.io

Open your browser and navigate to [https://n8n.io](https://n8n.io).

### Step 2: Click "Get Started Free"

On the homepage, click the **"Get Started Free"** button. This will redirect you to the signup page.

### Step 3: Sign Up

You have multiple options to create your account:

- **Email & Password** — Enter your email address, create a strong password, and provide your name.
- **Sign up with Google** — Click the Google option to use your Google account for quick signup.
- **Sign up with GitHub** — Click the GitHub option to authenticate via your GitHub account.

### Step 4: Verify Your Email

If you signed up with email, check your inbox for a verification email from n8n. Click the verification link to activate your account.

### Step 5: Complete Onboarding

Once verified, you'll be taken through a brief onboarding flow:

- Select your role (e.g., Developer, Product Manager, Marketing, etc.)
- Choose your primary use case
- Optionally invite team members

### Step 6: Access Your Cloud Instance

After onboarding, you'll be redirected to your personal n8n cloud instance (e.g., `https://your-name.app.n8n.cloud`). This is your workspace where you can start building workflows immediately.

### Cloud Plan Details

- **Free Trial** — 14 days with full features
- **Starter Plan** — Includes limited workflow executions per month
- **Pro Plan** — Higher execution limits, more workflows, and priority support
- **Enterprise Plan** — Custom pricing with SSO, advanced permissions, and dedicated support

> **Note:** Visit [https://n8n.io/pricing](https://n8n.io/pricing) for the most up-to-date pricing and plan details.

---

## Installing n8n Locally on macOS

### Prerequisites

Before installing n8n on macOS, ensure you have the following:

- **Node.js** (version 18 or higher) — Required runtime for n8n
- **npm** (comes bundled with Node.js) — Package manager
- **Terminal** access

### Method 1: Install via npm (Recommended)

#### Step 1: Install Node.js

If you don't already have Node.js installed:

**Option A — Using Homebrew (Recommended):**

```bash
# Install Homebrew if not already installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Node.js
brew install node
```

**Option B — Using the Official Installer:**

1. Go to [https://nodejs.org](https://nodejs.org)
2. Download the macOS installer (LTS version recommended)
3. Run the `.pkg` file and follow the installation wizard

#### Step 2: Verify Node.js Installation

```bash
node --version    # Should output v18.x or higher
npm --version     # Should output 9.x or higher
```

#### Step 3: Install n8n Globally

```bash
npm install n8n -g
```

This will download and install n8n along with all its dependencies. The installation may take a few minutes.

#### Step 4: Start n8n

```bash
n8n start
```

n8n will launch and be accessible at: **http://localhost:5678**

#### Step 5: (Optional) Run n8n with a Tunnel

If you need to access webhooks from external services during development:

```bash
n8n start --tunnel
```

This creates a temporary public URL that tunnels to your local instance.

### Method 2: Install via Docker on macOS

#### Step 1: Install Docker Desktop

1. Download Docker Desktop from [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. Install and launch Docker Desktop
3. Ensure Docker is running (check the whale icon in the menu bar)

#### Step 2: Run n8n with Docker

```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```

**Explanation of flags:**

- `-p 5678:5678` — Maps port 5678 on your machine to the container
- `-v ~/.n8n:/home/node/.n8n` — Persists your n8n data (workflows, credentials) between restarts
- `--rm` — Automatically removes the container when stopped

#### Step 3: Access n8n

Open your browser and go to: **http://localhost:5678**

---

## Installing n8n Locally on Windows

### Prerequisites

- **Node.js** (version 18 or higher)
- **npm** (bundled with Node.js)
- **Command Prompt** or **PowerShell** (or Windows Terminal)

### Method 1: Install via npm (Recommended)

#### Step 1: Install Node.js

1. Visit [https://nodejs.org](https://nodejs.org)
2. Download the **Windows Installer (.msi)** — LTS version recommended
3. Run the installer:
   - Accept the license agreement
   - Use default installation path (`C:\Program Files\nodejs\`)
   - Ensure **"Add to PATH"** is checked
   - Optionally check **"Automatically install the necessary tools"** (installs Chocolatey and build tools)
4. Click **Install** and wait for completion
5. Restart your terminal/command prompt

#### Step 2: Verify Node.js Installation

Open Command Prompt or PowerShell and run:

```powershell
node --version    # Should output v18.x or higher
npm --version     # Should output 9.x or higher
```

#### Step 3: Install Windows Build Tools (if needed)

Some n8n dependencies require native compilation. If you encounter build errors:

```powershell
npm install --global windows-build-tools
```

Or install Visual Studio Build Tools from [https://visualstudio.microsoft.com/visual-cpp-build-tools/](https://visualstudio.microsoft.com/visual-cpp-build-tools/).

#### Step 4: Install n8n Globally

```powershell
npm install n8n -g
```

Wait for the installation to complete. This may take several minutes.

#### Step 5: Start n8n

```powershell
n8n start
```

n8n will launch and be accessible at: **http://localhost:5678**

#### Step 6: (Optional) Run n8n with a Tunnel

```powershell
n8n start --tunnel
```

### Method 2: Install via Docker on Windows

#### Step 1: Install Docker Desktop

1. Download Docker Desktop from [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. Run the installer
3. During setup, ensure **WSL 2** backend is selected (recommended)
4. Restart your computer if prompted
5. Launch Docker Desktop and wait for it to initialize

#### Step 2: Run n8n with Docker

Open PowerShell and run:

```powershell
docker run -it --rm `
  --name n8n `
  -p 5678:5678 `
  -v n8n_data:/home/node/.n8n `
  docker.n8n.io/n8nio/n8n
```

> **Note:** On Windows, use backticks (`` ` ``) for line continuation in PowerShell, or put everything on one line.

#### Step 3: Access n8n

Open your browser and go to: **http://localhost:5678**

---

## First Launch & Verification

When you access n8n for the first time at `http://localhost:5678`, you'll be guided through an initial setup:

### Owner Account Setup

1. **Enter your details** — Provide your name, email, and create a password
2. **This creates the owner account** — The owner has full admin privileges on the local instance

### Verify the Installation

After setup, confirm everything is working:

1. **Create a test workflow** — Click "Add Workflow" in the top-right corner
2. **Add a Manual Trigger node** — This lets you run the workflow on demand
3. **Add a Set node** — Connect it to the trigger and configure it with a test value
4. **Execute the workflow** — Click "Test Workflow" and verify the output appears correctly

### Useful Environment Variables

You can customize n8n's behavior with environment variables:

| Variable | Description | Default |
|----------|-------------|---------|
| `N8N_PORT` | Port n8n runs on | `5678` |
| `N8N_PROTOCOL` | HTTP or HTTPS | `http` |
| `N8N_HOST` | Host name | `localhost` |
| `N8N_BASIC_AUTH_ACTIVE` | Enable basic auth | `false` |
| `N8N_BASIC_AUTH_USER` | Basic auth username | — |
| `N8N_BASIC_AUTH_PASSWORD` | Basic auth password | — |
| `DB_TYPE` | Database type | `sqlite` |
| `EXECUTIONS_DATA_SAVE_ON_ERROR` | Save error executions | `all` |

Set these before starting n8n:

**macOS / Linux:**
```bash
export N8N_PORT=8080
n8n start
```

**Windows (PowerShell):**
```powershell
$env:N8N_PORT = "8080"
n8n start
```

---

## Troubleshooting Common Issues

### Issue: "n8n: command not found" (macOS)

**Cause:** npm global bin directory is not in your PATH.

**Fix:**
```bash
export PATH="$PATH:$(npm config get prefix)/bin"
```
Add this line to your `~/.zshrc` or `~/.bash_profile` to make it permanent.

### Issue: "n8n is not recognized" (Windows)

**Cause:** Node.js or npm global directory is not in your system PATH.

**Fix:**
1. Open System Properties → Advanced → Environment Variables
2. Under "User variables", edit `Path`
3. Add: `C:\Users\<YourUsername>\AppData\Roaming\npm`
4. Restart your terminal

### Issue: Permission Errors on macOS

**Cause:** npm doesn't have write access to the global directory.

**Fix:**
```bash
sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}
```

Or configure npm to use a different directory:
```bash
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
export PATH=~/.npm-global/bin:$PATH
```

### Issue: Port 5678 Already in Use

**Fix:** Either stop the existing process or change the port:
```bash
# Find what's using the port
lsof -i :5678          # macOS
netstat -ano | findstr :5678   # Windows

# Use a different port
N8N_PORT=5679 n8n start
```

### Issue: Docker Container Fails to Start

**Common Fixes:**
1. Ensure Docker Desktop is running
2. Check if the port is already in use
3. Remove old containers: `docker rm -f n8n`
4. Pull the latest image: `docker pull docker.n8n.io/n8nio/n8n`

### Issue: Node.js Version Too Old

**Fix:** Update Node.js to version 18 or higher:
```bash
# macOS with Homebrew
brew upgrade node

# Windows — download latest from nodejs.org

# Using nvm (both platforms)
nvm install 18
nvm use 18
```

---

## Quick Reference Commands

| Action | macOS / Linux | Windows (PowerShell) |
|--------|--------------|---------------------|
| Install n8n | `npm install n8n -g` | `npm install n8n -g` |
| Start n8n | `n8n start` | `n8n start` |
| Start with tunnel | `n8n start --tunnel` | `n8n start --tunnel` |
| Update n8n | `npm update n8n -g` | `npm update n8n -g` |
| Check version | `n8n --version` | `n8n --version` |
| Custom port | `N8N_PORT=8080 n8n start` | `$env:N8N_PORT="8080"; n8n start` |

---

## Additional Resources

- **Official Documentation:** [https://docs.n8n.io](https://docs.n8n.io)
- **Community Forum:** [https://community.n8n.io](https://community.n8n.io)
- **GitHub Repository:** [https://github.com/n8n-io/n8n](https://github.com/n8n-io/n8n)
- **n8n Cloud:** [https://n8n.io](https://n8n.io)
- **Workflow Templates:** [https://n8n.io/workflows](https://n8n.io/workflows)

---
