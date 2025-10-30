# Troubleshooting Homebrew Installation on Mac

> Solutions for installing and troubleshooting Homebrew, the package manager for macOS.

## What is Homebrew?

Homebrew is a free and open-source package manager for macOS that makes it easy to install developer tools and applications from the command line. Think of it as an "app store for programming tools" where everything is free.

## Why Install Homebrew?

For Claude Code users and developers, Homebrew simplifies installation of:
- Python (via pyenv)
- Node.js (via nvm)
- Git
- GitHub CLI (gh)
- ripgrep (for Claude Code search features)
- Many other development tools

Instead of manually downloading and installing each tool, you can install them with simple commands like `brew install python`.

## Prerequisites

**Before installing Homebrew, you must install XCode Command Line Tools:**

```bash
xcode-select --install
```

See [XCode Troubleshooting](troubleshooting_xcode.md) if you have issues with this step.

## Installing Homebrew

### Installation Command

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### What Happens During Installation

1. Checks for XCode Command Line Tools (installs if missing)
2. Creates necessary directories
3. Downloads and installs Homebrew
4. Sets up the Homebrew repository
5. Displays "Next steps" instructions (important!)

### Critical Post-Installation Steps

After installation completes, you'll see instructions like this:

**For Apple Silicon Macs (M1, M2, M3, etc.):**
```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

**For Intel Macs:**
No additional steps needed - Homebrew installs to `/usr/local/bin` which is already in your PATH.

**IMPORTANT:** You must run these commands or Homebrew won't work! Copy and paste the exact commands shown in your terminal.

### Verifying Installation

```bash
# Check Homebrew version
brew --version

# Check installation health
brew doctor

# Verify Homebrew is in PATH
which brew
```

## Understanding the Apple Silicon Difference

### Apple Silicon Macs (M1/M2/M3)

- Homebrew installs to: `/opt/homebrew`
- Requires PATH configuration (the commands shown during installation)
- Must add to shell configuration: `~/.zprofile` or `~/.zshrc`

### Intel Macs

- Homebrew installs to: `/usr/local`
- Already in default PATH
- No additional configuration needed

To check your Mac type:
```bash
uname -m
# arm64 = Apple Silicon
# x86_64 = Intel
```

## Common Issues

### Issue: brew: command not found (Apple Silicon)

**Cause**: Forgot to run the post-installation PATH commands.

**Solution**:
```bash
# Add Homebrew to PATH
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zshrc

# Reload shell configuration
source ~/.zprofile
source ~/.zshrc

# Verify
brew --version
```

### Issue: brew: command not found (Intel Mac)

**Cause**: Installation failed or PATH issue.

**Solution**:
```bash
# Check if Homebrew is installed
ls -la /usr/local/bin/brew

# If it exists, add to PATH manually
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

# If it doesn't exist, reinstall Homebrew
```

### Issue: "Failed to connect to raw.githubusercontent.com"

**Cause**: Network/firewall blocking GitHub.

**Solution 1: Wait and retry**
```bash
# GitHub might be temporarily down
# Wait a few minutes and try again
```

**Solution 2: Check internet connection**
```bash
# Test GitHub connectivity
ping raw.githubusercontent.com
curl -I https://raw.githubusercontent.com
```

**Solution 3: Use different network**
- Try disabling VPN
- Try different WiFi network
- Try mobile hotspot

### Issue: "Permission denied" errors during installation

**Cause**: User doesn't have proper permissions for installation directories.

**Solution**:
```bash
# Homebrew handles this automatically in modern versions
# If you see this error, try:
sudo chown -R $(whoami) /usr/local/Homebrew

# Or for Apple Silicon:
sudo chown -R $(whoami) /opt/homebrew
```

### Issue: "XCode Command Line Tools not installed"

**Cause**: Missing prerequisite.

**Solution**:
```bash
# Install XCode Command Line Tools first
xcode-select --install

# Wait for installation to complete
# Then retry Homebrew installation
```

### Issue: brew doctor shows warnings

**Cause**: Various configuration issues.

**Common warnings and solutions:**

**"Warning: /usr/local/bin is not in your PATH"**
```bash
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

**"Warning: You have unlinked kegs in your Cellar"**
```bash
# Usually safe to ignore
# Or run: brew link [package-name]
```

**"Warning: Your XCode is outdated"**
```bash
# Update from App Store or ignore if not needed
```

### Issue: Installation hangs or is extremely slow

**Cause**: Slow internet connection or server issues.

**Solution**:
1. Be patient - initial installation can take 10-30 minutes
2. Check internet speed
3. Try different network
4. Cancel (Ctrl+C) and retry later

### Issue: After macOS update, Homebrew stops working

**Cause**: macOS updates sometimes break XCode Command Line Tools.

**Solution**:
```bash
# Reinstall Command Line Tools
sudo rm -rf /Library/Developer/CommandLineTools
xcode-select --install

# Then repair Homebrew
brew doctor
brew update
```

### Issue: Different shell (bash vs zsh)

**Modern Macs (Catalina+)**: Use zsh by default
**Older Macs**: Use bash by default

Check your shell:
```bash
echo $SHELL
```

**For zsh**: Add Homebrew to `~/.zshrc` or `~/.zprofile`
**For bash**: Add Homebrew to `~/.bash_profile`

## Using Homebrew: Basic Commands

### Installing Packages

```bash
# Install a package
brew install python

# Install multiple packages
brew install node git gh

# Search for a package
brew search ripgrep
```

### Updating and Upgrading

```bash
# Update Homebrew itself
brew update

# Upgrade all installed packages
brew upgrade

# Upgrade specific package
brew upgrade python
```

### Listing and Information

```bash
# List installed packages
brew list

# Get info about a package
brew info python

# See what packages are outdated
brew outdated
```

### Uninstalling

```bash
# Uninstall a package
brew uninstall python

# Uninstall and remove all versions
brew uninstall --force python
```

### Maintenance

```bash
# Check for issues
brew doctor

# Clean up old versions
brew cleanup

# See what would be cleaned up (dry run)
brew cleanup -n
```

## Essential Packages for Claude Code Users

After installing Homebrew, consider installing:

```bash
# Python version manager
brew install pyenv

# Node version manager (requires extra steps)
# See: https://github.com/nvm-sh/nvm

# Git (if not already installed)
brew install git

# GitHub CLI
brew install gh

# ripgrep (improves Claude Code search)
brew install ripgrep

# Useful utilities
brew install wget curl
```

## Homebrew vs Manual Installation

| Method | Pros | Cons |
|--------|------|------|
| **Homebrew** | Easy updates, manages dependencies, consistent locations | Requires learning brew commands |
| **Manual** | No dependencies, direct from source | Manual updates, inconsistent locations |

**For beginners with Claude Code**: Homebrew is recommended. It simplifies future installations and updates.

## Understanding Homebrew Directories

### Where Homebrew Installs Things

**Apple Silicon:**
- Homebrew itself: `/opt/homebrew`
- Packages: `/opt/homebrew/Cellar/`
- Symlinks: `/opt/homebrew/bin/`

**Intel:**
- Homebrew itself: `/usr/local/Homebrew`
- Packages: `/usr/local/Cellar/`
- Symlinks: `/usr/local/bin/`

### Why Symlinks Matter

Homebrew uses symlinks to make packages accessible. When you run `python3`, it might actually link to `/opt/homebrew/Cellar/python@3.12/3.12.0/bin/python3`.

## Uninstalling Homebrew

If you need to uninstall Homebrew (rarely needed):

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh)"
```

## Security Note

Homebrew installation requires admin (sudo) access during initial setup. The installation script is from Homebrew's official GitHub repository and is safe.

However:
- Always review what you're installing: `brew info [package]`
- Homebrew packages come from trusted sources
- Regularly update: `brew update && brew upgrade`

## Homebrew and Python/Node Installation

For Python and Node.js, there are multiple installation paths:

**Python:**
- Direct: `brew install python` (simple, works well)
- Via pyenv: `brew install pyenv` then `pyenv install 3.12.0` (more flexible)

**Node.js:**
- Direct: `brew install node` (simple)
- Via nvm: `brew install nvm` then use nvm (more flexible)

See [Python Troubleshooting](troubleshooting_python.md) and [Node.js Troubleshooting](troubleshooting_nodejs_nvm.md) for details.

## Getting More Help

- Official Homebrew docs: https://docs.brew.sh
- Homebrew GitHub: https://github.com/Homebrew/brew
- Community support: https://discourse.brew.sh
- Stack Overflow: Search "homebrew [your issue]"
- Ask in Cursor with error messages

## Next Steps

After successfully installing Homebrew:
1. Run `brew doctor` to verify everything is working
2. Install pyenv: `brew install pyenv`
3. Install other development tools as needed
4. Consider installing ripgrep: `brew install ripgrep`
5. Proceed with Python and Node.js installation
6. Install Claude Code using the native installer
