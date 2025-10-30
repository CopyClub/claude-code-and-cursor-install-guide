# Complete Installation Guide for Mac

> Step-by-step guide to installing Claude Code and all necessary tools for Mac users who are new to development.

## Overview

This guide will help you install Claude Code and recommended tools to use it effectively, even if you've never done any programming before.

### Quick Start (Minimum Installation)

To get Claude Code running quickly:
1. Cursor (optional but helpful for troubleshooting)
2. **Claude Code** (10-15 minutes)

That's it! You can start using Claude Code immediately.

### Full Installation (Recommended)

For the best experience, also install:
3. XCode Command Line Tools (needed for many development tools)
4. Homebrew (makes installing other tools easier)
5. Python (highly recommended for Claude Code workflows)
6. Node.js (optional, only if you plan to do web development)

**Estimated time**:
- Quick start: 15-30 minutes
- Full installation: 1-2 hours (mostly waiting for downloads)

## Before You Start

### Check Your Mac Type

You need to know if you have an Apple Silicon Mac (M1/M2/M3) or an Intel Mac:

1. Click the Apple menu (top left)
2. Select "About This Mac"
3. Look at the "Chip" or "Processor" line:
   - If it says "Apple M1", "M2", or "M3" → **Apple Silicon**
   - If it says "Intel" → **Intel Mac**

**Write this down** - you'll need it during installation.

### What You'll Need

- Mac with macOS 10.15 (Catalina) or newer
- Admin password for your Mac
- Stable internet connection
- At least 10 GB free disk space

## Step 1: Install Cursor (Optional but Recommended)

Cursor is an AI-powered code editor that can help you troubleshoot any errors you encounter during this installation process.

### Why Install Cursor First?

When you run into errors or confusing terminal messages during installation, you can:
1. Copy the error message
2. Paste it into Cursor
3. Ask Cursor what it means and how to fix it

It's like having a helpful assistant throughout the installation process.

### Installation Steps

1. Visit the Cursor website (search "Cursor IDE" in your browser)
2. Download the Mac version
3. Open the downloaded .dmg file
4. Drag Cursor to your Applications folder
5. Open Cursor from Applications

**If you encounter issues**: See [Cursor Troubleshooting](troubleshooting/troubleshooting_cursor.md)

## Step 2: Install Claude Code

Now let's install Claude Code using the native installer - it's simple and doesn't require Node.js!

### Installation

Open Terminal (found in Applications > Utilities) and run:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

### What Happens

1. The script downloads and installs Claude Code
2. It installs to `~/.local/bin/claude`
3. It adds Claude Code to your PATH automatically
4. Takes 2-5 minutes

### Verify Installation

```bash
# Check Claude Code version
claude --version

# Check installation health
claude doctor
```

### First Run

```bash
# Start Claude Code
claude
```

You'll be prompted to:
1. Authenticate with your Anthropic account
2. Accept permissions
3. Choose your preferences

**Success!** You now have Claude Code installed and can start using it immediately!

### If you encounter issues

See [Claude Code Troubleshooting](troubleshooting/troubleshooting_claude_install.md)

Common issues:
- **"claude: command not found"**: Close and reopen Terminal, or run `source ~/.zshrc`
- **Permission errors**: Make sure you didn't use sudo
- **PATH issues**: See [PATH Configuration Troubleshooting](troubleshooting/troubleshooting_path_config.md)

### Can I stop here?

**Yes!** Claude Code is now installed and ready to use. The remaining steps install additional tools that enhance your experience but aren't required.

**When to continue:**
- If Claude Code asks you to install additional tools (like XCode Command Line Tools)
- If you want to run Python scripts that Claude Code generates
- If you plan to do regular development work

---

## Optional but Recommended: Additional Tools

The following steps install tools that greatly enhance your Claude Code experience. These are not required for Claude Code to work, but will make your experience much better.

---

## Step 3: Install XCode Command Line Tools

XCode Command Line Tools provide essential development utilities that many tools depend on. Homebrew (next step) will install these automatically, but you can install them first for a cleaner setup.

### Installation

In Terminal, run:

```bash
xcode-select --install
```

### What Happens

1. A popup window appears asking to install
2. Click "Install"
3. Accept the license agreement
4. Wait 10-40 minutes for download and installation
5. You'll see "The software was installed"

### Verify Installation

```bash
xcode-select -p
# Should show: /Library/Developer/CommandLineTools
```

**If you encounter issues**: See [XCode Troubleshooting](troubleshooting/troubleshooting_xcode.md)

**Note**: If you skip this step, Homebrew (next step) will install XCode Command Line Tools automatically.

---

## Step 4: Install Homebrew

Homebrew is a "package manager" - it makes installing other development tools much easier.

### Installation

In Terminal, copy and paste this entire command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Press Enter and provide your Mac password when prompted.

### Critical Next Steps

After installation completes, Terminal will show "Next steps". **You must follow these instructions!**

**For Apple Silicon Macs (M1/M2/M3)**, you'll see something like:
```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

**Copy and run these exact commands** that appear in your terminal.

**For Intel Macs**, you typically don't need additional steps.

### Verify Installation

```bash
brew --version
```

You should see the Homebrew version number.

```bash
brew doctor
```

Should say "Your system is ready to brew" (warnings are usually okay).

**If you encounter issues**: See [Homebrew Troubleshooting](troubleshooting/troubleshooting_homebrew.md)

---

## Step 5: Install Python with pyenv

Python is a programming language you'll use frequently with Claude Code. We'll install it using pyenv, which avoids the frustrating "python vs python3" problem.

### Why pyenv?

Without pyenv, you'd have to type `python3` for every command. AI tools like Claude expect `python` (without the 3), so you'd constantly need to fix generated code. pyenv solves this.

### Installation

```bash
# Install pyenv via Homebrew
brew install pyenv

# Add pyenv to your shell configuration
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc

# Reload your shell configuration
source ~/.zshrc
```

### Install Python

```bash
# Install latest Python 3 (this will take several minutes)
pyenv install 3.12.0

# Set it as your default Python
pyenv global 3.12.0
```

### Verify Installation

```bash
# Check Python version
python --version

# Should show: Python 3.12.0 (not python3!)
# Check where Python is installed
which python

# Should show: /Users/[yourname]/.pyenv/shims/python
```

**Success**: You can now use `python` (not `python3`) for all commands!

**If you encounter issues**: See [Python Troubleshooting](troubleshooting/troubleshooting_python.md)

---

## Step 6: Install Node.js (Optional)

Node.js is only needed if you plan to do web development or use npm packages. **You already installed Claude Code**, so this is completely optional.

### Should You Install Node.js?

**Skip this step if**:
- You just want Claude Code working (use native installer)
- You want the simplest installation path

**Complete this step if**:
- You plan to do web development
- You want to use npm for Claude Code
- You want maximum flexibility

### Installation with nvm (Recommended)

```bash
# Install nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Add to shell configuration
echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.zshrc
echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.zshrc

# Reload shell
source ~/.zshrc

# Install latest LTS Node.js
nvm install --lts

# Set as default
nvm alias default node
```

### Verify Installation

```bash
node --version
npm --version
```

**If you encounter issues**: See [Node.js and nvm Troubleshooting](troubleshooting/troubleshooting_nodejs_nvm.md)

---

## Step 7: Configure Cursor to Use Claude Code

If you installed Cursor, you can set it up to use Claude Code:

1. Open Cursor
2. Open Settings (Cmd+,)
3. Search for "terminal.integrated.defaultProfile.osx"
4. Verify it's set to use zsh or bash

Now you can open a terminal in Cursor and run `claude` directly!

---

## Step 8: Install Additional Tools (Optional)

### GitHub CLI (for Git integration)

```bash
brew install gh
```

### ripgrep (improves Claude Code search)

```bash
brew install ripgrep
```

## Verification Checklist

After completing all steps, verify everything works:

```bash
# Check each tool
cursor --version          # If you installed Cursor
xcode-select -p          # Should show: /Library/Developer/CommandLineTools
brew --version           # Should show Homebrew version
python --version         # Should show: Python 3.12.0
pip --version            # Should work
node --version           # If you installed Node.js
npm --version            # If you installed Node.js
claude --version         # Should show Claude Code version
claude doctor            # Should report healthy installation
```

## Common Issues and Solutions

### Issue: "command not found" errors

**Solution**: You likely forgot to reload your shell configuration.

```bash
# Reload your shell configuration
source ~/.zshrc

# Or close and reopen Terminal
```

See [PATH Configuration Troubleshooting](troubleshooting/troubleshooting_path_config.md) for more help.

### Issue: Permission errors

**Solution**: Don't use `sudo`! If you see permission errors:
1. Check which installation method you used
2. Consider using native installers instead of npm
3. See specific troubleshooting guides for each tool

### Issue: brew: command not found (Apple Silicon)

**Solution**: You forgot the post-installation steps for Homebrew.

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zshrc
source ~/.zshrc
```

### Issue: python3 works but not python

**Solution**: pyenv didn't set up properly.

```bash
# Check pyenv status
pyenv versions

# Set global version
pyenv global 3.12.0

# Reload shell
source ~/.zshrc
```

## Understanding Your Terminal and Shell

### What is the Terminal?

Terminal is an application that lets you type commands to control your Mac. You'll use it frequently with Claude Code.

**To open Terminal:**
1. Press Cmd+Space to open Spotlight
2. Type "Terminal"
3. Press Enter

### What is a Shell?

The shell is the program that runs inside Terminal and interprets your commands. Modern Macs use **zsh** by default.

Check your shell:
```bash
echo $SHELL
```

### Configuration Files

Your shell settings are stored in `~/.zshrc` (for zsh) or `~/.bash_profile` (for bash).

When we add paths and configurations, we're modifying these files.

## Next Steps

After completing this installation:

1. **Test Claude Code**: Try generating a simple Python script
2. **Explore Cursor**: Ask it questions about programming
3. **Learn basic terminal commands**: cd, ls, pwd, mkdir
4. **Join the community**: Find Claude Code Discord/forums for help
5. **Read the docs**: Visit Claude Code documentation for features

## Getting Help

If you encounter issues not covered in this guide:

1. **Use Cursor**: Paste error messages and ask for help
2. **Check specific troubleshooting guides**: Links throughout this document
3. **Run diagnostics**: `claude doctor` for Claude Code issues
4. **Ask in community forums**: Share error messages and system info

## Maintenance and Updates

### Keeping Everything Updated

Run these commands periodically:

```bash
# Update Homebrew and all packages
brew update && brew upgrade

# Update Python
pyenv install 3.12.1  # (when new version available)
pyenv global 3.12.1

# Update Node.js (if using nvm)
nvm install --lts
nvm alias default node

# Claude Code updates automatically (if installed correctly)
# Or manually: claude update
```

### When to Reinstall

You rarely need to reinstall anything. If you do:

1. Check the specific troubleshooting guide first
2. Try `brew doctor` to diagnose issues
3. Only reinstall as a last resort

## Troubleshooting Guides Reference

- [Cursor Installation](troubleshooting/troubleshooting_cursor.md)
- [XCode Command Line Tools](troubleshooting/troubleshooting_xcode.md)
- [Homebrew](troubleshooting/troubleshooting_homebrew.md)
- [Python and pyenv](troubleshooting/troubleshooting_python.md)
- [Node.js and nvm](troubleshooting/troubleshooting_nodejs_nvm.md)
- [PATH Configuration](troubleshooting/troubleshooting_path_config.md)
- [Claude Code Installation](troubleshooting/troubleshooting_claude_install.md)

## Congratulations!

You've successfully set up a complete development environment on your Mac. You're now ready to use Claude Code to build amazing things!
