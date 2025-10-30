# Troubleshooting Git Bash Installation on Windows

> Solutions for common issues when installing Git Bash on Windows.

## What is Git Bash?

Git Bash is a terminal application for Windows that provides a Unix-like command-line environment. It comes included with Git for Windows and is the recommended terminal for using Claude Code on Windows.

## Why Git Bash for Claude Code?

Many Windows users experience issues when running Claude Code in PowerShell or Command Prompt. Git Bash provides:

1. **Unix-like commands**: Works the same way as Mac/Linux terminals
2. **Better compatibility**: Fewer issues with npm and Node.js commands
3. **Standard environment**: Most Claude Code documentation assumes a Unix-like shell
4. **Fewer PATH issues**: Better handling of environment variables

## Installation Steps

### Download Git for Windows

1. Visit the official Git website: https://git-scm.com/download/win
2. The download should start automatically
3. Alternatively, visit https://gitforwindows.org for the official Git for Windows project

### Run the Installer

1. Run the downloaded installer (.exe file)
2. Follow the Git Setup wizard

### Important Installation Options

During installation, you'll see several configuration screens. Here are the recommended settings:

#### Editor Selection
- Choose your preferred editor (the default is Vim, but Nano or your preferred editor is fine)
- If unsure, select "Use Notepad as Git's default editor"

#### PATH Environment
- Select **"Git from the command line and also from 3rd-party software"** (recommended)
- This adds Git to your Windows PATH for all applications

#### Line Ending Conversions
- Select **"Checkout Windows-style, commit Unix-style line endings"** (recommended)

#### Terminal Emulator
- Select **"Use MinTTY (the default terminal of MSYS2)"** (recommended)
- This provides the best Git Bash experience

#### Default Branch Name
- Select **"Override the default branch name for new repositories"** and use "main"

### Complete Installation

1. Continue clicking "Next" through the remaining options
2. Click "Install"
3. Click "Finish" when installation completes

## Launching Git Bash

After installation, you can open Git Bash by:

1. **Start Menu**: Search for "Git Bash" and click it
2. **Right-click menu**: Right-click in any folder and select "Git Bash Here"
3. **Desktop shortcut**: Create a shortcut if desired

## Common Issues

### Git Bash doesn't open or crashes immediately

**Solution:**
1. Restart your computer after installation
2. Try running as Administrator (right-click > Run as administrator)
3. Reinstall Git for Windows with default settings

### Commands not recognized (command not found)

**Solution:**
1. Verify Git was added to PATH during installation
2. Open Windows Settings > System > About > Advanced system settings
3. Click "Environment Variables"
4. Check that Git paths are in the System PATH:
   - `C:\Program Files\Git\cmd`
   - `C:\Program Files\Git\bin`
5. Restart Git Bash after PATH changes

### Permission denied errors

**Solution:**
1. Right-click Git Bash shortcut and select "Run as administrator"
2. Check file/folder permissions in Windows Explorer
3. Ensure you're not trying to access protected system directories

### Git Bash vs PowerShell: Which should I use?

For Claude Code, **Git Bash is strongly recommended** because:

- It provides better compatibility with Unix-style commands
- Fewer PATH-related issues
- Most documentation assumes a bash-like environment
- Easier troubleshooting when working with Claude Code support

However, PowerShell is also supported. See the [PATH Configuration Troubleshooting](troubleshooting_path_config.md) guide if you prefer PowerShell.

### npm or node commands not working in Git Bash

**Solution:**
1. Verify Node.js is installed (see [Node.js and nvm Troubleshooting](troubleshooting_nodejs_nvm.md))
2. Check that Node.js is in your Windows PATH
3. Restart Git Bash after installing Node.js
4. Test with: `node --version` and `npm --version`

### Git Bash terminal looks strange or has display issues

**Solution:**
1. Right-click the title bar > Options
2. Adjust the font, colors, and window size under "Looks"
3. Try changing the theme from "Text" settings
4. Increase font size if text is too small

### Can't paste into Git Bash

**Solution:**
- Use **Shift+Insert** to paste (not Ctrl+V)
- Or right-click in the terminal window and select Paste
- You can configure Ctrl+Shift+V in Options > Keys

### Git Bash uses wrong version of Node/npm

This can happen if you have multiple installations.

**Solution:**
1. Check which version is being used: `which node` and `which npm`
2. Verify your PATH order in Environment Variables
3. Consider using nvm (Node Version Manager) - see [Node.js Troubleshooting](troubleshooting_nodejs_nvm.md)

## Configuration Tips

### Set Git Bash as default terminal in Cursor

1. Open Cursor
2. Go to Settings (Ctrl+,)
3. Search for "terminal.integrated.defaultProfile.windows"
4. Select "Git Bash"

### Customize Git Bash appearance

1. Right-click the Git Bash title bar > Options
2. Explore the settings for:
   - Font size and style
   - Color schemes
   - Cursor appearance
   - Transparency

### Create a desktop shortcut

1. Navigate to: `C:\Program Files\Git\git-bash.exe`
2. Right-click and select "Create shortcut"
3. Move the shortcut to your desktop

## Alternative: Using claude.bat

If you continue to experience PATH issues with Claude Code in Git Bash:

1. Some users have success using `claude.bat` instead of `claude` command
2. This is not ideal but can be a workaround
3. See [PATH Configuration Troubleshooting](troubleshooting_path_config.md) for better solutions

## Getting More Help

- Official Git for Windows documentation: https://gitforwindows.org
- Git documentation: https://git-scm.com/doc
- Stack Overflow: Search for your specific error message

## Next Steps

After successfully installing Git Bash:
1. Install Node.js and npm (see [Node.js Troubleshooting](troubleshooting_nodejs_nvm.md))
2. Configure your PATH properly (see [PATH Configuration Troubleshooting](troubleshooting_path_config.md))
3. Install Claude Code using the native Windows installer
