# Complete Installation Guide for Windows

> Step-by-step guide to installing Claude Code and all necessary tools for Windows users who are new to development.

## Overview

This guide will help you install Claude Code and recommended tools to use it effectively, even if you've never done any programming before.

### Quick Start (Minimum Installation)

To get Claude Code running quickly:
1. Cursor (optional but helpful for troubleshooting)
2. Git Bash (provides better terminal support)
3. **Claude Code** (15-20 minutes total)

That's it! You can start using Claude Code immediately.

### Full Installation (Recommended)

For the best experience, also install:
4. Python (highly recommended for Claude Code workflows)
5. Node.js (optional, only if you plan to do web development)

**Estimated time**:
- Quick start: 20-30 minutes
- Full installation: 1-2 hours (mostly waiting for downloads)

## Before You Start

### System Requirements

- Windows 10 or Windows 11
- Admin access to your computer
- Stable internet connection
- At least 10 GB free disk space

### Important: Which Terminal to Use?

Windows has several terminal options:
- **Command Prompt** (cmd.exe)
- **PowerShell**
- **Git Bash** (we'll install this)

**For Claude Code, we strongly recommend Git Bash** because:
- Better compatibility with Unix-style commands
- Fewer PATH-related issues
- Most documentation assumes a bash-like environment
- Easier troubleshooting

## Step 1: Install Cursor (Optional but Recommended)

Cursor is an AI-powered code editor that can help you troubleshoot any errors you encounter during this installation process.

### Why Install Cursor First?

When you run into errors or confusing messages during installation, you can:
1. Copy the error message
2. Paste it into Cursor
3. Ask Cursor what it means and how to fix it

It's like having a helpful assistant throughout the installation process.

### Installation Steps

1. Visit the Cursor website (search "Cursor IDE" in your browser)
2. Download the Windows version
   - Most systems use **x64** architecture
   - ARM-based devices should choose **arm64**
3. Run the installer
4. Follow the setup wizard
5. Launch Cursor

**If you encounter issues**: See [Cursor Troubleshooting](troubleshooting/troubleshooting_cursor.md)

## Step 2: Install Git Bash

Git Bash provides a Unix-like command-line environment on Windows, which makes Claude Code work much more reliably.

### Installation

1. Visit https://git-scm.com/download/win
2. Download should start automatically
3. Run the installer
4. **Follow these important settings during installation:**

#### Key Installation Settings

**Choosing the default editor:**
- Select "Use Notepad as Git's default editor" (or your preference)

**Adjusting your PATH environment:**
- Select **"Git from the command line and also from 3rd-party software"** (recommended)

**Choosing the SSH executable:**
- Keep the default (Use bundled OpenSSH)

**Choosing HTTPS transport backend:**
- Keep the default (Use the OpenSSL library)

**Configuring line ending conversions:**
- Select **"Checkout Windows-style, commit Unix-style line endings"**

**Configuring the terminal emulator:**
- Select **"Use MinTTY (the default terminal of MSYS2)"** (recommended)

**Default branch name:**
- Select **"Override the default branch name for new repositories"** and use "main"

**Other options:**
- Keep default settings for remaining options

5. Click "Install"
6. Click "Finish"

### Verify Installation

1. Search for "Git Bash" in Windows Start menu
2. Open Git Bash
3. You should see a terminal window

**If you encounter issues**: See [Git Bash Troubleshooting](troubleshooting/troubleshooting_git_bash.md)

## Step 3: Install Claude Code

Now let's install Claude Code! We'll use the native installer which is simpler and more reliable than the npm version.

### Installation

**Option 1: Using PowerShell (Recommended)**

1. Search for "PowerShell" in Windows Start menu
2. Open PowerShell (no need for admin)
3. Run this command:

```powershell
irm https://claude.ai/install.ps1 | iex
```

**Option 2: Using Git Bash**

Open Git Bash and run:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

### What Happens

1. The script downloads and installs Claude Code
2. It installs to `%USERPROFILE%\.local\bin\claude`
3. It adds Claude Code to your PATH automatically
4. Takes 2-5 minutes

### Verify Installation

Open **Git Bash** and run:

```bash
# Check Claude Code version
claude --version

# Check installation health
claude doctor
```

### First Run

In Git Bash:
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

**Problem: "claude: command not found"**

**Solution 1**: Restart Git Bash
- Close all Git Bash windows
- Open a new Git Bash window
- Try `claude --version` again

**Solution 2**: Check PATH
1. Right-click "This PC" > Properties
2. Advanced system settings > Environment Variables
3. Check User PATH includes: `C:\Users\[YourName]\.local\bin`
4. If missing, add it and restart Git Bash

**Solution 3**: Use full path temporarily
```bash
~/.local/bin/claude
```

See [Claude Code Troubleshooting](troubleshooting/troubleshooting_claude_install.md) for more help.

### Can I stop here?

**Yes!** Claude Code is now installed and ready to use. The remaining steps install additional tools that enhance your experience but aren't required.

**When to continue:**
- If you want to run Python scripts that Claude Code generates
- If you plan to do regular development work
- If Claude Code recommends installing additional tools

---

## Optional but Recommended: Additional Tools

The following steps install tools that greatly enhance your Claude Code experience. These are not required for Claude Code to work, but will make your experience much better.

---

## Step 4: Install Python

Python is a programming language you'll use frequently with Claude Code.

### Installation

1. Visit https://www.python.org/downloads/
2. Download the latest Python 3 installer (Windows installer 64-bit)
3. Run the installer
4. **CRITICAL**: Check **"Add Python to PATH"** at the bottom
5. Click **"Install Now"**
6. Wait for installation to complete
7. Click "Close"

### Verify Installation

Open **Git Bash** (not PowerShell or Command Prompt) and run:

```bash
python --version
pip --version
```

You should see version numbers for both.

**If you encounter issues**: See [Python Troubleshooting](troubleshooting/troubleshooting_python.md)

### Alternative: pyenv-win (Advanced)

If you want more control over Python versions (similar to pyenv on Mac), you can install pyenv-win:

```powershell
# Open PowerShell as Administrator and run:
Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"
&"./install-pyenv-win.ps1"

# Then in a new PowerShell:
pyenv install 3.12.0
pyenv global 3.12.0
```

For most users, the simple Python installer is sufficient.

---

## Step 5: Install Node.js (Optional)

Node.js is only needed if you plan to do web development or use npm packages. **You already installed Claude Code**, so this is completely optional.

### Should You Install Node.js?

**Skip this step if**:
- You just want Claude Code working (use native installer)
- You want the simplest installation path

**Complete this step if**:
- You plan to do web development
- You want to use npm for Claude Code
- You want maximum flexibility

### Option A: Simple Installation (Recommended for Beginners)

1. Visit https://nodejs.org
2. Download the LTS (Long Term Support) version
3. Run the .msi installer
4. **Check "Automatically install the necessary tools"** during setup
5. Follow the installation wizard
6. Restart Git Bash

### Option B: Install with nvm-windows (Advanced)

**Important: Uninstall any existing Node.js first**

1. Go to Settings > Apps > Installed apps
2. Uninstall Node.js if present
3. Restart your computer
4. Visit https://github.com/coreybutler/nvm-windows/releases
5. Download `nvm-setup.zip` from the latest release
6. Extract and run `nvm-setup.exe`
7. **During installation, change the symlink path to avoid spaces**: Use `C:\nvm\nodejs`
8. Complete installation
9. Restart Git Bash

**Then install Node.js:**

```bash
# List available versions
nvm list available

# Install latest LTS (e.g., 20.10.0)
nvm install 20.10.0

# Use that version
nvm use 20.10.0
```

### Verify Installation

In Git Bash:
```bash
node --version
npm --version
```

**If you encounter issues**: See [Node.js and nvm Troubleshooting](troubleshooting/troubleshooting_nodejs_nvm.md)

---

## Step 6: Configure Cursor to Use Git Bash

If you installed Cursor, set it up to use Git Bash as the default terminal:

1. Open Cursor
2. Go to Settings (Ctrl+,)
3. Search for "terminal.integrated.defaultProfile.windows"
4. Select **"Git Bash"**

Now you can open a terminal in Cursor and run `claude` directly!

---

## Step 7: Install Additional Tools (Optional)

### GitHub CLI (for Git integration)

In Git Bash:
```bash
# Download from: https://cli.github.com
# Or via winget in PowerShell:
winget install --id GitHub.cli
```

### ripgrep (improves Claude Code search)

In PowerShell:
```powershell
winget install BurntSushi.ripgrep.MSVC
```

---

## Understanding PATH on Windows

PATH configuration on Windows can be challenging. Here's what you need to know:

### What is PATH?

PATH tells Windows where to find programs when you type commands. When you type `claude`, Windows searches through all directories in your PATH.

### Viewing Your PATH

**In PowerShell:**
```powershell
$env:PATH
```

**In Git Bash:**
```bash
echo $PATH
```

### Common PATH Locations for Our Tools

After installation, your PATH should include:
- `C:\Program Files\Git\cmd` (Git)
- `C:\Users\[YourName]\AppData\Local\Programs\Python\Python312` (Python)
- `C:\Users\[YourName]\AppData\Local\Programs\Python\Python312\Scripts` (pip)
- `C:\Program Files\nodejs` (Node.js, if installed)
- `C:\Users\[YourName]\.local\bin` (Claude Code native install)
- Or `C:\Users\[YourName]\AppData\Roaming\npm` (Claude Code via npm)

### When to Restart

**After any PATH changes, you MUST:**
1. Close ALL terminal windows (Git Bash, PowerShell, Command Prompt)
2. Close and restart any IDEs (Cursor, VS Code)
3. In some cases, restart your computer

**If you encounter PATH issues**: See [PATH Configuration Troubleshooting](troubleshooting/troubleshooting_path_config.md)

---

## Verification Checklist

After completing all steps, verify everything works in **Git Bash**:

```bash
# Check each tool
cursor --version          # If you installed Cursor
git --version            # Should work
python --version         # Should show Python 3.x
pip --version            # Should work
node --version           # If you installed Node.js
npm --version            # If you installed Node.js
claude --version         # Should show Claude Code version
claude doctor            # Should report healthy installation
```

## Common Issues and Solutions

### Issue: "command not found" in Git Bash

**Solution 1: Restart Git Bash**
Close all Git Bash windows and open a new one.

**Solution 2: Check PATH**
```bash
# See if the command is in PATH
which python
which claude
```

If it returns nothing, the tool isn't in your PATH. See [PATH Configuration Troubleshooting](troubleshooting/troubleshooting_path_config.md).

**Solution 3: Use full path**
```bash
# Example for Python
/c/Users/[YourName]/AppData/Local/Programs/Python/Python312/python.exe --version
```

### Issue: Commands work in PowerShell but not Git Bash

**Cause**: Different PATH configurations.

**Solution**: Set PATH in Windows Environment Variables (affects both):
1. Right-click "This PC" > Properties
2. Advanced system settings > Environment Variables
3. Edit User or System PATH
4. Add necessary directories
5. Restart ALL terminals

### Issue: Permission errors

**Solution**: Don't run Git Bash as Administrator unless absolutely necessary. Most tools should install in your user directory.

### Issue: Git Bash is slow or unresponsive

**Solutions**:
1. Disable antivirus temporarily during installations
2. Check for Windows updates
3. Try PowerShell as an alternative (though Git Bash is generally better for Claude Code)

## Understanding Windows Terminals

### Git Bash vs PowerShell vs Command Prompt

| Feature | Git Bash | PowerShell | Command Prompt |
|---------|----------|------------|----------------|
| **Best for Claude Code** | Yes | Maybe | No |
| **Unix commands** | Yes | Limited | No |
| **PATH issues** | Fewer | More | More |
| **Learning curve** | Easy | Moderate | Easy |

**Recommendation**: Use Git Bash for Claude Code and development work.

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

**Python:**
Download and install new versions from python.org

**Node.js (if using nvm-windows):**
```bash
nvm install --lts
nvm use --lts
```

**Git:**
Run the installer again with the new version

**Claude Code:**
Updates automatically with native installer, or:
```bash
npm update -g @anthropic-ai/claude-code  # If installed via npm
```

### When to Reinstall

You rarely need to reinstall anything. If you do:

1. Check the specific troubleshooting guide first
2. Try `claude doctor` to diagnose issues
3. Only reinstall as a last resort

## Troubleshooting Guides Reference

- [Cursor Installation](troubleshooting/troubleshooting_cursor.md)
- [Git Bash](troubleshooting/troubleshooting_git_bash.md)
- [Python Installation](troubleshooting/troubleshooting_python.md)
- [Node.js and nvm](troubleshooting/troubleshooting_nodejs_nvm.md)
- [PATH Configuration](troubleshooting/troubleshooting_path_config.md)
- [Claude Code Installation](troubleshooting/troubleshooting_claude_install.md)

## Windows-Specific Tips

### Using Git Bash Effectively

**Copy and paste:**
- **Right-click** to paste (or Shift+Insert)
- Select text and **Ctrl+Insert** to copy
- Or configure Ctrl+Shift+C/V in Options

**Navigate to a folder:**
```bash
cd /c/Users/YourName/Documents
```

**Open current directory in File Explorer:**
```bash
explorer .
```

### Working with Windows Paths

Windows uses backslashes (`\`) but Git Bash uses forward slashes (`/`):

```bash
# Git Bash style (preferred in Git Bash)
cd /c/Users/YourName/Documents

# Windows style (works but not recommended)
cd C:\Users\YourName\Documents
```

### Dealing with Spaces in Paths

If a path has spaces, use quotes:

```bash
cd "/c/Program Files/MyApp"
python "/c/My Documents/script.py"
```

## Alternative: Using WSL (Windows Subsystem for Linux)

Some users prefer WSL for development. It provides a full Linux environment on Windows.

**Pros:**
- True Linux environment
- Better compatibility with Unix tools
- Often faster for certain operations

**Cons:**
- More complex setup
- Additional troubleshooting needed
- File system performance considerations

For beginners, **Git Bash is simpler and sufficient** for Claude Code.

If you want to explore WSL, see the [Claude Code WSL documentation](troubleshooting/troubleshooting_claude_install.md#windows-installation-issues-errors-in-wsl).

## Congratulations!

You've successfully set up a complete development environment on Windows. You're now ready to use Claude Code to build amazing things!
