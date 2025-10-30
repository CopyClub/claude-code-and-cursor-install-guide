# Claude Code Installation Guides for Non-Developers

Complete installation guides and troubleshooting documentation for installing Claude Code on Mac and Windows, designed specifically for users who don't have typical developer tools installed.

## Quick Start

Choose your operating system:

- **[Mac Installation Guide](installation_guide_mac.md)** - Complete setup for macOS users
- **[Windows Installation Guide](installation_guide_windows.md)** - Complete setup for Windows users

These guides walk you through everything from scratch, assuming you have no development tools installed yet.

## What's Different About These Guides?

Most Claude Code tutorials assume you already have:
- Node.js and npm installed
- Homebrew (Mac) or package managers (Windows)
- Basic understanding of PATH configuration
- Familiarity with terminal commands

**These guides assume none of that.** They start from the beginning and explain each step in detail.

## Installation Overview

### Quick Start: Minimum Installation

**Mac:**
1. [Cursor](troubleshooting/troubleshooting_cursor.md) (optional but helpful)
2. **[Claude Code](troubleshooting/troubleshooting_claude_install.md)** ← Start here!

**Windows:**
1. [Cursor](troubleshooting/troubleshooting_cursor.md) (optional but helpful)
2. [Git Bash](troubleshooting/troubleshooting_git_bash.md)
3. **[Claude Code](troubleshooting/troubleshooting_claude_install.md)**

**Time**: 15-30 minutes. You can start using Claude Code immediately!

### Full Installation: Recommended Tools

**Mac:**
1. [Cursor](troubleshooting/troubleshooting_cursor.md) (optional but recommended)
2. **[Claude Code](troubleshooting/troubleshooting_claude_install.md)**
3. [XCode Command Line Tools](troubleshooting/troubleshooting_xcode.md) (optional, for other dev tools)
4. [Homebrew](troubleshooting/troubleshooting_homebrew.md) (optional, for other dev tools)
5. [Python with pyenv](troubleshooting/troubleshooting_python.md) (optional, highly recommended)
6. [Node.js with nvm](troubleshooting/troubleshooting_nodejs_nvm.md) (optional, for web dev)

**Windows:**
1. [Cursor](troubleshooting/troubleshooting_cursor.md) (optional but recommended)
2. [Git Bash](troubleshooting/troubleshooting_git_bash.md)
3. **[Claude Code](troubleshooting/troubleshooting_claude_install.md)**
4. [Python](troubleshooting/troubleshooting_python.md) (optional, highly recommended)
5. [Node.js with nvm-windows](troubleshooting/troubleshooting_nodejs_nvm.md) (optional, for web dev)

**Time**: 1-2 hours total

## Why Install Cursor First?

We recommend installing [Cursor](troubleshooting/troubleshooting_cursor.md) before starting because:
- It's an AI-powered code editor that can help troubleshoot errors
- When you encounter confusing terminal messages, you can paste them into Cursor for help
- It provides a friendly environment for working with Claude Code later

## Key Insights from Experience

These guides address common issues we've encountered when helping non-technical users:

### The sudo Problem
**Never use `sudo npm install -g`** for Claude Code. This causes:
- Permission issues
- Broken auto-updates
- PATH configuration problems

**Solution**: Use the native installer instead, which doesn't require sudo.

### The python vs python3 Problem (Mac)
On Mac, AI tools generate code using `python`, but you have to type `python3`. This gets frustrating quickly.

**Solution**: Use [pyenv](troubleshooting/troubleshooting_python.md) to set `python` as the default command for Python 3.

### The PATH Challenge
PATH configuration is surprisingly difficult, especially on Windows. It seems like every installation needs a different approach.

**Solution**: We've created comprehensive [PATH troubleshooting documentation](troubleshooting/troubleshooting_path_config.md) that covers both platforms and common scenarios.

### Git Bash on Windows
Many Windows users experience issues with PowerShell when using Claude Code.

**Solution**: We recommend [Git Bash](troubleshooting/troubleshooting_git_bash.md) for better compatibility and fewer PATH issues.

### The Native Windows Version
The npm-installed version of Claude Code has known issues on Windows.

**Solution**: Use the [native Windows installer](troubleshooting/troubleshooting_claude_install.md) for better reliability.

## Complete Documentation Index

### Main Installation Guides

- [Mac Installation Guide](installation_guide_mac.md) - Complete setup for macOS
- [Windows Installation Guide](installation_guide_windows.md) - Complete setup for Windows

### Platform-Specific Troubleshooting

#### Mac-Specific
- [XCode Command Line Tools](troubleshooting/troubleshooting_xcode.md)
- [Homebrew](troubleshooting/troubleshooting_homebrew.md)

#### Windows-Specific
- [Git Bash](troubleshooting/troubleshooting_git_bash.md)

#### Common to Both Platforms
- [Cursor Installation](troubleshooting/troubleshooting_cursor.md)
- [Python Installation](troubleshooting/troubleshooting_python.md)
- [Node.js and nvm](troubleshooting/troubleshooting_nodejs_nvm.md)
- [PATH Configuration](troubleshooting/troubleshooting_path_config.md)
- [Claude Code Installation](troubleshooting/troubleshooting_claude_install.md)

## Should You Install Node.js?

**Short answer**: Only if you want to use the npm installer for Claude Code.

**Recommendation**: Use the native installer instead, which doesn't require Node.js:

**Mac/Linux/Git Bash:**
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**Windows PowerShell:**
```powershell
irm https://claude.ai/install.ps1 | iex
```

However, if you plan to do web development, Node.js is useful. See the [Node.js troubleshooting guide](troubleshooting/troubleshooting_nodejs_nvm.md) for details.

## Should You Use Version Managers?

### pyenv (Python Version Manager)

**Recommendation: Yes, especially on Mac**

Reasons:
- Fixes the python vs python3 problem
- Avoids permission issues
- Professional best practice
- Makes working with AI tools smoother

See [Python Troubleshooting](troubleshooting/troubleshooting_python.md) for details.

### nvm (Node Version Manager)

**Recommendation: Only if you're doing web development**

For simple Claude Code use, the native installer is better. If you need Node.js, nvm helps avoid permission issues.

See [Node.js Troubleshooting](troubleshooting/troubleshooting_nodejs_nvm.md) for details.

## Common Issues Across All Installations

### Issue: "command not found"

This is almost always a PATH issue. See [PATH Configuration Troubleshooting](troubleshooting/troubleshooting_path_config.md).

**Quick fixes:**
1. Restart your terminal
2. Check PATH with: `echo $PATH` (Mac/Git Bash) or `$env:PATH` (PowerShell)
3. Verify the tool is installed: `which [command]` or `where [command]`

### Issue: Permission errors

**Never use sudo** for npm installations or Python package installations.

**Solutions:**
- Use native installers when available
- Use version managers (pyenv, nvm)
- Install in user directories, not system directories

### Issue: Changes don't take effect

**Solution**: Restart everything after configuration changes:
1. Close all terminal windows
2. Restart any IDEs (Cursor, VS Code)
3. In extreme cases, restart your computer

## Understanding the Tools

### What is a Package Manager?

A package manager installs and updates software from the command line.

- **Mac**: Homebrew
- **Windows**: We don't use one (installer files instead)

### What is a Terminal/Shell?

A terminal is where you type commands to control your computer.

- **Mac**: Terminal app (uses zsh or bash)
- **Windows**: Git Bash (recommended), PowerShell, or Command Prompt

### What is PATH?

PATH tells your computer where to find programs. When you type `claude`, your computer searches through PATH to find the claude program.

Most installation problems are PATH problems. See [PATH Configuration](troubleshooting/troubleshooting_path_config.md).

## Getting Help

If you encounter issues not covered in these guides:

1. **Use Cursor**: Paste error messages and ask for explanations
2. **Check troubleshooting guides**: Use the index above to find relevant guides
3. **Run diagnostics**: `claude doctor` checks Claude Code health
4. **Community forums**: Share your specific error and system information
5. **GitHub Issues**: Report bugs at https://github.com/anthropics/claude-code/issues

## Contributing Feedback

These guides are based on real experiences helping non-technical users install Claude Code. If you:
- Find errors or unclear instructions
- Encounter issues not covered here
- Have suggestions for improvements

Please share your feedback to help improve these guides for others.

## Version Information

These guides were last updated for:
- Claude Code: 2025 versions
- macOS: 10.15 (Catalina) and newer
- Windows: 10 and 11
- Python: 3.12.x
- Node.js: 20.x LTS

## Quick Reference Commands

### Check Versions

```bash
# Claude Code
claude --version
claude doctor

# Python
python --version

# Node.js (if installed)
node --version
npm --version

# Git
git --version

# Mac-specific
brew --version
xcode-select -p

# Check PATH
echo $PATH              # Mac/Git Bash
$env:PATH              # PowerShell
```

### Common Installation Commands

**Mac:**
```bash
# XCode Command Line Tools
xcode-select --install

# Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# pyenv
brew install pyenv

# Claude Code (native)
curl -fsSL https://claude.ai/install.sh | bash
```

**Windows:**
```bash
# In Git Bash or PowerShell

# Claude Code (native)
# PowerShell:
irm https://claude.ai/install.ps1 | iex

# Git Bash:
curl -fsSL https://claude.ai/install.sh | bash
```

## What's Next?

After successfully installing Claude Code:

1. **Learn basic terminal commands**: `cd`, `ls`, `pwd`, `mkdir`
2. **Test Claude Code**: Generate a simple Python script
3. **Explore features**: Try different Claude Code capabilities
4. **Join the community**: Connect with other users
5. **Read the official docs**: Explore advanced features

## License and Attribution

These guides compile information from:
- Official Claude Code documentation
- Official installation guides for various tools
- Real-world troubleshooting experiences
- Community feedback and testing

All external links point to official documentation and trusted sources.

## Acknowledgments

These guides were created to address real challenges encountered when helping non-technical users set up Claude Code. Special thanks to all the users who provided feedback on what worked and what didn't during their installation process.
