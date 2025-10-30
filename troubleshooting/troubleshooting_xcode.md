# Troubleshooting XCode Command Line Tools Installation

> Solutions for installing and troubleshooting XCode Command Line Tools on Mac.

## What are XCode Command Line Tools?

XCode Command Line Tools are a collection of development utilities for macOS, including:
- Compilers (gcc, clang)
- Make and build tools
- Git version control
- Headers and libraries for development

## Why Do You Need Them?

Many Mac development tools require XCode Command Line Tools, including:
- **Homebrew**: Won't work without them
- **pyenv**: Needs compilers to build Python versions
- **Various npm packages**: Some native modules require compilation
- **gh CLI**: GitHub's command-line tool depends on them

When installing Homebrew or other development tools, you'll often see them install XCode Command Line Tools automatically.

## Do You Need the Full XCode App?

**No, usually not.**

There are two different things:
1. **XCode Command Line Tools** (~1.2GB) - What you need for most development
2. **Full XCode IDE** (~12GB+) - Only needed for iOS/macOS app development

For Claude Code and general development, **Command Line Tools alone are sufficient**.

## Three Ways to Install

### Method 1: Terminal Command (Recommended)

This is the quickest and most straightforward method:

```bash
xcode-select --install
```

**What happens:**
1. A software update popup window appears
2. Click "Install" button
3. Agree to the license agreement
4. Download begins (1.2GB)
5. Installation completes automatically

**Installation time:**
- Fast internet (100Mbps) with M1 Mac: ~8 minutes
- Slower connections or Intel Macs: 20-40 minutes

### Method 2: Install via Homebrew (Automatic)

When you install Homebrew, it will automatically install XCode Command Line Tools if not present.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Homebrew's installer will detect if Command Line Tools are missing and install them for you.

### Method 3: Manual Download from Apple

1. Go to https://developer.apple.com/download/all/
2. Sign in with your Apple ID
3. Search for "Command Line Tools"
4. Download the version matching your macOS version
5. Install the downloaded .dmg package

**When to use this method:**
- The `xcode-select --install` command fails
- You have a slow internet connection and want to download elsewhere
- You need a specific older version

## Verifying Installation

Check if XCode Command Line Tools are installed:

```bash
xcode-select -p
```

**If installed**, you'll see:
```
/Library/Developer/CommandLineTools
```

**If not installed**, you'll see:
```
xcode-select: error: unable to get active developer directory...
```

Check the version:
```bash
xcode-select --version
```

Check specific tools:
```bash
gcc --version
git --version
make --version
```

## Common Issues

### Issue: "xcode-select: error: command line tools are already installed"

**Cause**: Tools are already installed.

**Solution**: You're all set! Verify with `xcode-select -p`

If you need to reinstall:
```bash
# Remove existing installation
sudo rm -rf /Library/Developer/CommandLineTools

# Reinstall
xcode-select --install
```

### Issue: "Can't install the software because it is not currently available"

**Cause**: Software update servers are having issues, or your macOS needs updating.

**Solution**:
1. Check for macOS updates: System Preferences > Software Update
2. Update macOS if available
3. Try again after updating
4. Or use the manual download method from Apple's developer site

### Issue: Installation window doesn't appear

**Cause**: System preferences or popup blockers.

**Solution**:
1. Try running with sudo: `sudo xcode-select --install`
2. Check System Preferences > Security & Privacy for blocked installations
3. Use the manual download method instead

### Issue: "xcrun: error: invalid active developer path"

**Cause**: Command Line Tools not installed or corrupted.

**Solution**:
```bash
# Try installing
xcode-select --install

# If that fails, install via manual download
# Or install full XCode from App Store, then:
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
```

### Issue: Installation fails midway or hangs

**Solution**:
1. Cancel the installation
2. Restart your Mac
3. Remove partial installation:
   ```bash
   sudo rm -rf /Library/Developer/CommandLineTools
   ```
4. Try installing again
5. If still failing, use manual download method

### Issue: "You have not agreed to the Xcode license agreements"

**Cause**: License agreement not accepted.

**Solution**:
```bash
sudo xcodebuild -license accept
```

Or run it interactively to read the license:
```bash
sudo xcodebuild -license
# Press space to scroll, type 'agree' at the end
```

### Issue: After macOS update, command line tools stop working

**Cause**: Major macOS updates sometimes break or remove Command Line Tools.

**Solution**:
```bash
# Reinstall Command Line Tools
sudo rm -rf /Library/Developer/CommandLineTools
xcode-select --install
```

### Issue: "git" or "gcc" command not found after installation

**Cause**: PATH issue or installation incomplete.

**Solution**:
1. Verify installation: `xcode-select -p`
2. If shows correct path, restart Terminal
3. Check PATH includes: `/usr/bin`
4. Try resetting:
   ```bash
   sudo xcode-select --reset
   ```

## What Gets Installed

After installation, you'll have access to:

**Compilers and Build Tools:**
- clang (C/C++ compiler)
- gcc (GNU compiler)
- make
- cmake
- ld (linker)

**Version Control:**
- git
- svn

**Development Headers:**
- Standard C libraries
- macOS SDK headers

**Other Utilities:**
- python3 (basic version)
- perl
- Various Unix utilities

## XCode Command Line Tools vs Full XCode

| Feature | Command Line Tools | Full XCode |
|---------|-------------------|------------|
| Size | ~1.2GB | ~12GB+ |
| Installation Time | 8-40 minutes | 1-3 hours |
| Use Case | General development | iOS/macOS app development |
| Includes IDE | No | Yes |
| Includes Simulators | No | Yes |
| Required for Homebrew | Yes | Not necessary |
| Required for Claude Code | Yes | Not necessary |

## Keeping Tools Updated

XCode Command Line Tools update automatically with macOS Software Updates.

To manually check for updates:
```bash
softwareupdate --list
softwareupdate --install --all
```

Or use System Preferences > Software Update.

## Uninstalling XCode Command Line Tools

If you need to uninstall (rarely needed):

```bash
sudo rm -rf /Library/Developer/CommandLineTools
```

Then reinstall if needed:
```bash
xcode-select --install
```

## When Do You Need Full XCode?

Install the full XCode app only if:
- You're developing iOS or macOS apps
- You need the Interface Builder or Storyboards
- You need the iOS Simulator
- A specific tool explicitly requires the full XCode

Download from Mac App Store or https://developer.apple.com/xcode/

## XCode Command Line Tools and Homebrew

**Important:** Install XCode Command Line Tools **before** installing Homebrew.

Homebrew will automatically install them if missing, but it's cleaner to install them first:

```bash
# 1. Install XCode Command Line Tools
xcode-select --install

# 2. Verify installation
xcode-select -p

# 3. Then install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Getting More Help

- Apple Developer Documentation: https://developer.apple.com/xcode/
- Stack Overflow: Search for your specific error
- XCode Command Line Tools FAQ: https://www.junian.net/dev/xcode-command-line-tools-installation-faq/
- Ask in Cursor with your error messages

## Next Steps

After successfully installing XCode Command Line Tools:
1. Install Homebrew (see [Homebrew Troubleshooting](troubleshooting_homebrew.md))
2. Install other development tools (Python, Node.js, etc.)
3. Install Claude Code
4. Verify git works: `git --version`
