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

#### Install Conda

[Conda](https://docs.anaconda.com/free/miniconda/index.html) is an open-source package management and environment management system for any language:
```bash
brew install --cask miniconda
```
```bash
conda init "$(basename "${SHELL}")"
```

#### Developer Tools

CLI tools for managing AWS services and Oracle Cloud
```bash
brew install awscli oci-cli
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
brew install hashicorp/tap/terraform ansible ansible-lint helm
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

File type identification library:
```bash
brew install libmagic
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
### 6. Install Node Version Manager (NVM)

To manage multiple versions of Node.js, use NVM.

[Install NVM](https://github.com/nvm-sh/nvm?tab=readme-ov-file#install--update-script)

Install Node.js latest LTS version:
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
### 10. Install Essential Apps from the App Store

- Coffee Buzz - keeping your Mac awake
- Xcode - developing apps


---
### 11. Install Other Applications

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
    - [Forklift](https://binarynights.com/) - dual pane file manager and file transfer client `brew install --cask forklift`
- Proton
    - [Pass](https://proton.me/pass/) - password manager `brew install --cask proton-pass`
    - [Drive](https://proton.me/drive/) - cloud drive `brew install --cask proton-drive`
    - [Mail](https://proton.me/mail/) - mail client `brew install --cask proton-mail`
    - [VPN](https://protonvpn.com/) - No logs, No ads, Unlimited & free forever `brew install --cask protonvpn`
