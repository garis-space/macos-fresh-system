# Setting Up a Fresh System: A Step-by-Step Guide

When you're setting up a new Mac, there are a bunch of essential steps and tools that can help enhance your experience and productivity.

:warning: Before starting the installation of a fresh system, make sure to copy your SSH keys, AWS CLI configurations, kubectl configurations, and VPN profiles from your old system.

Here’s a comprehensive guide to get your system ready from scratch.


### 1. Show Hidden Files in Finder

To make hidden files visible in Finder:
```bash
defaults write com.apple.finder AppleShowAllFiles true
```
```bash
killall Finder
```


---
### 2. Install Homebrew

Homebrew is a package manager for macOS. It simplifies the installation of software on the Mac operating system, and also installs the Xcode Command Line Tools if they are not already present.

[Install Brew here](https://brew.sh/)

Optionally, you can turn off sending anonymous analytics `brew analytics off`

Add maintenance function to keep fast update/upgrade/clean brew packages, use this as `upd` in terminal:
```bash
cat << 'EOF' >> ~/.zshrc

# Homebrew maintenance function
upd() {
  local GREEN="\033[1;32m"
  local YELLOW="\033[1;33m"
  local BLUE="\033[1;34m"
  local NC="\033[0m"

  echo "${BLUE}=== 🔄 Updating Homebrew ===${NC}"
  brew update || return 1

  echo "\n${BLUE}=== ⬆️ Upgrading ===${NC}"
  brew upgrade

  echo "\n${BLUE}=== 🧹 Cleaning ===${NC}"
  brew autoremove
  brew cleanup

  echo "\n${BLUE}=== 🩺 Doctor ===${NC}"
  brew doctor

  echo "\n${GREEN}✅ Done.${NC}\n"
}
EOF
```


---
### 3. Configure Your Terminal

To improve your terminal experience, install [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh):
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```


---
### 4. Install and Configure Powerlevel10k

[Powerlevel10k](https://github.com/romkatv/powerlevel10k) is a fast and flexible Zsh theme that provides prompt customization. Here’s how to install and configure it along with the necessary fonts:

#### Install Fonts for Powerlevel10k

For an enhanced terminal visual experience, manually install the optional fonts from the Powerlevel10k repository:
- **Manual Font Installation**: Visit the [Powerlevel10k GitHub page](https://github.com/romkatv/powerlevel10k?tab=readme-ov-file#manual-font-installation) and follow the instructions to download and install the MesloLGS NF family.
- **Apple Terminal**: Go to Terminal → Preferences → Profiles → Text, click Change under Font, and select MesloLGS NF family.
- **Visual Studio Code**: Go to File → Preferences → Settings (PC) or Code → Preferences → Settings (Mac), enter `terminal.integrated.fontFamily` in the search box, and set the value to `MesloLGS NF`.

#### Install Powerlevel10k

You can install Powerlevel10k using Homebrew:
```bash
brew install powerlevel10k
```
```bash
echo "source $(brew --prefix)/share/powerlevel10k/powerlevel10k.zsh-theme" >>~/.zshrc
```

#### Configure Powerlevel10k

After installation, configure Powerlevel10k to suit your preferences:
```bash
p10k configure
```
This script will guide you through the setup process, allowing you to choose various prompt elements to match your workflow and aesthetic preferences.


---
### 5. Install Essential Brew Packages

Install the necessary tools via Homebrew:

#### Install uv

[uv](https://docs.astral.sh/uv/) is extremely fast Python package and project manager, written in Rust.:
```bash
brew install uv
```
Add alias to your ~/.zshrc
```bash
echo 'alias activate="source .venv/bin/activate"' >> ~/.zshrc
```

#### Install Conda

[Conda](https://docs.anaconda.com/free/miniconda/index.html) is an open-source package management and environment management system for any language:
```bash
brew install --cask miniconda
```
```bash
conda init "$(basename "${SHELL}")"
```

#### Developer Tools

CLI tools for managing AWS services, Oracle Cloud and Hetzner Cloud
```bash
brew install awscli oci-cli hcloud
```

CLI tool controlling Kubernetes clusters:
```bash
brew install kubectl
```

Tools specifically useful for DevOps roles:
```bash
brew tap hashicorp/tap
```
```bash
brew install hashicorp/tap/terraform ansible ansible-lint helm argocd
```

[Tilt](https://tilt.dev) for dev microservice environment on Kubernetes
```bash
brew install tilt
```

PostgreSQL client library, necessary for Django projects connecting to PostgreSQL databases using psycopg:
```bash
brew install libpq
```
```bash
echo 'export PATH="/opt/homebrew/opt/libpq/bin:$PATH"' >> ~/.zshrc
```

Tool for internationalizing applications:
```bash
brew install gettext
```

File type identification library and utility to optimize graphic files:
```bash
brew install libmagic jpegoptim optipng
```

[Rust](https://www.rust-lang.org) programming language
```bash
brew install rust
```

Tool for converting HTML/CSS documents to PDF:
```bash
brew install weasyprint
```

[Postman](https://www.postman.com) is an API platform for building and using APIs:
```bash
brew install --cask postman
```

[Sourcetree](https://www.sourcetreeapp.com) beautiful Git GUI:
```bash
brew install --cask sourcetree
```

[Wireshark](https://www.wireshark.org) is network protocol analyzer:
```bash
brew install --cask wireshark
```

[Snyk](https://snyk.io) is tool for scans and monitors projects for security vulnerabilities:
```bash
brew install snyk-cli
```

Command-line JSON processor:
```bash
brew install jq
```

#### Office Tools

[ONLYOFFICE](https://www.onlyoffice.com/) document management:
```bash
brew install --cask onlyoffice
```

#### To upgrade all installed packages to the latest:

```bash
brew update
```
```bash
brew upgrade
```


---
### 6. Install Node using Node Version Manager (NVM)

To manage multiple versions of Node.js, use NVM.

[Install Node using nvm](https://nodejs.org/en/download)

Download and Install Node.js latest LTS version:
```bash
nvm install --lts
```

To upgrade Node.js to the latest LTS version:
```bash
nvm install 'lts/*' --reinstall-packages-from=current
```


---
### 7. Install Docker

For container management, [Docker](https://hub.docker.com/editions/community/docker-ce-desktop-mac/) is essential. After installing Docker, you should adjust its settings for optimal performance:
```
brew install --cask docker
```

- In Docker's settings, disable **Automatically check configuration** to prevent it from checking your configuration for unexpected changes made by other applications.
- Adjust the **Resources** settings (CPU and Memory) according to the capabilities of your machine to ensure Docker does not exhaust all system resources.


---
### 8. Set Up Your IDE

[Visual Studio Code](https://code.visualstudio.com) is a lightweight but powerful source code editor. Install it along with some useful extensions:
```bash
brew install --cask visual-studio-code
```


---
### 9. Install a VPN Client

For secure internet access and privacy:

- [Tunnelblick](https://tunnelblick.net/): A free and open-source VPN client for macOS.
```bash
brew install --cask tunnelblick
```

- [ProtonVPN](https://protonvpn.com/): No logs, No ads, Unlimited & free forever

---
### 10. Claude Code

Claude Code is an AI-powered code assistant that helps you write, understand, and debug code more efficiently:

- [Claude Code](https://www.anthropic.com/claude-code/)
```bash
brew install --cask claude-code
```

By creating separate sessions for personal and work use, you can keep your projects organized and maintain a clear distinction between different contexts:

Create directories for work Claude sessions (personal settings are located in ~/.claude dir)
```bash
mkdir -p ~/.claude-work
```

Add alias to .zshrc for easy access to work Claude sessions (the `grep` guard keeps the alias from being added twice when you rerun this step)
```bash
grep -q 'alias claude-work=' ~/.zshrc || echo 'alias claude-work="CLAUDE_CONFIG_DIR=$HOME/.claude-work claude"' >> ~/.zshrc
```

Reload .zshrc to apply changes
```bash
source ~/.zshrc
```

First run of alias will create separate Claude sessions for work use.

To check which account each session uses, look at `email` and `orgName` (`loggedIn` alone does not tell the accounts apart):
```bash
claude-work auth status
```
```bash
claude auth status
```

NOTE: Commands started from inside a `claude-work` session (e.g. `!claude auth status`) inherit `CLAUDE_CONFIG_DIR`, so they report the work account too.

NOTE: Claude Code keeps the login in the macOS Keychain under a name derived from the `CLAUDE_CONFIG_DIR` value. Set it to the same absolute path everywhere (`/Users/<you>/.claude-work`), otherwise you end up with a separate login. Places that do not expand `~` or `$HOME` need the full path written out.

NOTE: Your home directory is a parent of every project, so `claude-work` sessions also load `~/.claude/rules/` as project rules. Anything you put there reaches the work account as well.



---
### 11. Codex CLI

Codex CLI is OpenAI's coding agent that runs in your terminal:

- [OpenAI Codex CLI](https://developers.openai.com/codex/cli)
```bash
brew install --cask codex
```

Same as with Claude Code, you can create separate sessions for personal and work use. Codex keeps its settings, login and session history in the directory pointed to by `CODEX_HOME` (personal settings are located in ~/.codex dir).

Create directory for work Codex sessions (unlike Claude Code, Codex does not create it on first run and exits with `CODEX_HOME points to ... but that path does not exist`)
```bash
mkdir -p ~/.codex-work
```

Add alias to .zshrc for easy access to work Codex sessions (the `grep` guard keeps the alias from being added twice when you rerun this step)
```bash
grep -q 'alias codex-work=' ~/.zshrc || echo 'alias codex-work="CODEX_HOME=$HOME/.codex-work codex"' >> ~/.zshrc
```

Reload .zshrc to apply changes
```bash
source ~/.zshrc
```

Log in with your work account (opens the browser; if the browser is signed in to your personal ChatGPT, sign out there first or the login lands on the personal account):
```bash
codex-work login
```

`codex-work login status` prints only `Logged in using ChatGPT`, the same for every account. To see which account and plan a directory is logged in with, decode the id token:
```bash
jq -c '.tokens.id_token | split(".")[1] | gsub("-";"+") | gsub("_";"/") | @base64d | fromjson | {email, plan: .["https://api.openai.com/auth"].chatgpt_plan_type}' ~/.codex-work/auth.json
```
Swap the path for `~/.codex/auth.json` to check the personal one.

NOTE: Profiles in `config.toml` (`codex --profile <name>`) only switch settings like model or approval policy, not the login. Every `CODEX_HOME` holds exactly one login, so separate accounts need separate directories.

Lock the work sessions to your company ChatGPT workspace, so they can't be logged in with a personal account by mistake. First confirm with the command above that the login shows your work email and plan; locking a wrong first login pins the personal account instead. Then read the workspace id:
```bash
jq -r '.tokens.account_id' ~/.codex-work/auth.json
```

And add it to `~/.codex-work/config.toml`:
```toml
forced_login_method = "chatgpt"
forced_chatgpt_workspace_id = "<workspace-id>"
```

NOTE: The `claude-work` and `codex-work` aliases work only in the terminal. IDE extensions and desktop apps always use the default (personal) directories ~/.claude and ~/.codex.



---
### 12. Install Essential Apps from the App Store

- Xcode - developing apps


---
### 13. Install Other Applications

- Password manager
    - [Bitwarden](https://bitwarden.com/) `brew install --cask bitwarden`
    - [1Password](https://1password.com) `brew install --cask 1password`
    - [Enpass](https://www.enpass.io/) `brew install --cask enpass`
- Web browser
    - [Firefox](https://www.mozilla.org/) `brew install --cask firefox`
    - [Google Chrome](https://www.google.com/chrome/) `brew install --cask google-chrome`
    - [Microsoft Edge](https://www.microsoft.com/edge/) `brew install --cask microsoft-edge`
- Team communication
    - [Slack](https://slack.com/) `brew install --cask slack`
    - [Discord](https://discord.com/) `brew install --cask discord`
    - [Microsoft Teams](https://www.microsoft.com/en/microsoft-teams/group-chat-software/) `brew install --cask microsoft-teams`
    - [WhatsApp](https://www.whatsapp.com/) `brew install --cask whatsapp`
- Multimedia player
    - [VLC Media Player](https://www.videolan.org/vlc/) `brew install --cask vlc`
    - [Spotify](https://www.spotify.com/) `brew install --cask spotify` 
- File manager
    - [Bloom](https://bloomapp.club/) - dual pane file manager and file transfer client `brew install --cask bloom`
- Proton
    - [Pass](https://proton.me/pass/) - password manager `brew install --cask proton-pass`
    - [Drive](https://proton.me/drive/) - cloud drive `brew install --cask proton-drive`
    - [Mail](https://proton.me/mail/) - mail client `brew install --cask proton-mail`
    - [VPN](https://protonvpn.com/) - No logs, No ads, Unlimited & free forever `brew install --cask protonvpn`
- AI Desktop Clients
    - [Claude](https://claude.com) `brew install claude`
    - [ChatGPT](https://chatgpt.com) `brew install chatgpt`
- AI Coding Agent
    - [Claude Code CLI](https://www.anthropic.com/claude-code) `brew install --cask claude-code` (NOTE: installed in point #10)
    - [OpenAI Codex CLI](https://developers.openai.com/codex/cli) `brew install --cask codex` (NOTE: installed in point #11)
    - [Google Gemini AI CLI](https://github.com/google-gemini/gemini-cli) `brew install gemini-cli`
    - [GitHub Copilot](https://docs.github.com/en/copilot) `brew install copilot-cli`
- Tools
    - [KeepingYouAwake](https://github.com/newmarcel/KeepingYouAwake) `brew install keepingyouawake`
