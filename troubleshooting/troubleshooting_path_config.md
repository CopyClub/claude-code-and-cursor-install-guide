# Troubleshooting PATH Configuration

> Solutions for common PATH-related issues on Mac and Windows.

## What is PATH?

The PATH is an environment variable that tells your operating system where to look for executable programs. When you type a command like `claude` or `python`, your system searches through the directories listed in your PATH to find the program.

## Why PATH Matters for Claude Code

Proper PATH configuration is essential for Claude Code because:

1. **Command accessibility**: Allows you to run `claude` from any directory
2. **Tool discovery**: Claude Code needs to find npm, node, python, and other tools
3. **Auto-updates**: Claude Code's auto-update feature requires correct permissions and PATH setup

## Understanding PATH Issues

The most common PATH-related problems:

- `command not found` or `'claude' is not recognized`
- Commands work in one terminal but not another
- Need to use full paths like `/usr/local/bin/claude` instead of just `claude`
- Installing with `sudo npm install` causes permission and PATH issues

## Mac PATH Configuration

### How to View Your Current PATH

Open Terminal and run:
```bash
echo $PATH
```

You'll see a colon-separated list of directories like:
```
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

### Default Shell: zsh vs bash

- **macOS Catalina (10.15) and newer**: Uses `zsh` by default
- **Older macOS versions**: Used `bash` by default

Check your shell with:
```bash
echo $SHELL
```

### Configuration Files

Your PATH is set in shell configuration files:

**For zsh (modern Macs):**
- `~/.zshrc` - Run for every new terminal session
- `~/.zprofile` - Run at login

**For bash (older Macs):**
- `~/.bash_profile` - Run at login
- `~/.bashrc` - Run for every new terminal session

### Common Mac PATH Issues

#### Issue: Command works one time but not after restart

**Cause**: You set PATH in the terminal, but didn't add it to your configuration file.

**Solution**: Add to `~/.zshrc` (or `~/.bash_profile` for bash):
```bash
export PATH="$PATH:/path/to/directory"
```

Then reload your configuration:
```bash
source ~/.zshrc
```

#### Issue: ~/.zshrc or ~/.zprofile doesn't exist

**Solution**: Create the file:
```bash
touch ~/.zshrc
```

Then add your PATH configuration and reload.

#### Issue: Changes to PATH don't take effect

**Solution**:
1. Close all Terminal windows
2. Open a new Terminal window
3. Verify changes with: `echo $PATH`

#### Issue: PATH is empty or missing standard directories

**Solution**: Reset to default PATH by adding to `~/.zshrc`:
```bash
export PATH="/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
```

### Recommended PATH Order for Mac

PATH directories are searched in order. Put custom installations first:

```bash
# Recommended order
export PATH="$HOME/.local/bin:$PATH"                    # Claude Code local installation
export PATH="/opt/homebrew/bin:$PATH"                   # Homebrew (Apple Silicon)
export PATH="/usr/local/bin:$PATH"                      # Homebrew (Intel Mac)
export PATH="$HOME/.nvm/versions/node/[version]/bin:$PATH"  # nvm
```

### Special Considerations for Apple Silicon Macs

Homebrew installs to `/opt/homebrew` on Apple Silicon, which is NOT in the default PATH.

**Solution**: Add to `~/.zshrc`:
```bash
# For Apple Silicon Macs
eval "$(/opt/homebrew/bin/brew shellenv)"
```

## Windows PATH Configuration

### How to View Your Current PATH

**PowerShell:**
```powershell
$env:PATH
```

**Git Bash:**
```bash
echo $PATH
```

**Command Prompt:**
```cmd
echo %PATH%
```

### Configuration Locations

Windows PATH is stored in:
- **System PATH**: Applies to all users (requires admin)
- **User PATH**: Applies only to your user account

### How to Edit PATH in Windows

#### GUI Method (Recommended for Beginners)

1. Right-click "This PC" or "Computer" on desktop
2. Select "Properties"
3. Click "Advanced system settings" (left sidebar)
4. Click "Environment Variables" button
5. In the "User variables" section, select "Path"
6. Click "Edit"
7. Click "New" to add a new directory
8. Enter the full path (e.g., `C:\Program Files\nodejs`)
9. Click "OK" on all dialogs
10. **Restart all terminals and applications**

#### PowerShell Method

To add a directory to User PATH:
```powershell
[Environment]::SetEnvironmentVariable("Path", $env:Path + ";C:\path\to\directory", "User")
```

### Common Windows PATH Issues

#### Issue: PATH changes don't take effect

**Cause**: Windows doesn't reload environment variables automatically.

**Solution**:
1. Close ALL terminal windows (Git Bash, PowerShell, Command Prompt)
2. Close and restart any IDEs (Cursor, VS Code)
3. In extreme cases, restart your computer

#### Issue: 'claude' is not recognized as a command

**Solution**:
1. Find where Claude Code is installed:
   - Native installation: `%USERPROFILE%\.local\bin`
   - npm installation: `%APPDATA%\npm`
2. Add that directory to your PATH using the GUI method above
3. Restart all terminal windows

#### Issue: PATH is too long (Windows limitation)

**Cause**: Windows has a 2048-character limit for PATH.

**Solution**:
1. Remove unnecessary entries from PATH
2. Use shorter directory names where possible
3. Consider using symbolic links for long paths

#### Issue: Using claude.bat instead of claude

**Cause**: Windows isn't finding the `claude` executable properly.

**Better solution**: Fix your PATH instead of using `.bat`:
1. Locate claude installation directory
2. Add it to PATH properly
3. Restart terminal
4. Test with: `where claude`

#### Issue: PowerShell PATH different from Git Bash PATH

**Cause**: Git Bash translates Windows paths to Unix-style.

**Solution**:
- Set PATH in Windows Environment Variables (affects both)
- Don't try to set PATH separately in Git Bash config
- Both should respect Windows Environment Variables

### Special Considerations for PowerShell

PowerShell has both a **User PATH** and a **System PATH** that get combined.

To see just your User PATH:
```powershell
[Environment]::GetEnvironmentVariable("Path", "User")
```

To see System PATH:
```powershell
[Environment]::GetEnvironmentVariable("Path", "Machine")
```

### Windows PATH Best Practices

1. **Use User PATH when possible**: Doesn't require admin rights
2. **No spaces**: Avoid paths with spaces when possible
3. **Use quotes**: If path has spaces, Windows should handle it, but test thoroughly
4. **Restart terminals**: Always restart after PATH changes
5. **Check order**: Earlier entries in PATH take priority

## Verifying PATH is Correct

### Test if a command is in your PATH

**Mac/Linux/Git Bash:**
```bash
which claude
which node
which python
```

**Windows PowerShell:**
```powershell
where.exe claude
where.exe node
where.exe python
```

### Test if PATH contains a directory

**Mac/Linux/Git Bash:**
```bash
echo $PATH | grep "/directory/to/check"
```

**Windows PowerShell:**
```powershell
$env:PATH -split ';' | Select-String "directory\\to\\check"
```

## Avoiding sudo Installation Issues

One of the most common causes of PATH problems is installing Claude Code with `sudo npm install -g`.

### Why sudo Causes Problems

1. **Wrong ownership**: Files are owned by root instead of your user
2. **Auto-update breaks**: Claude Code can't update itself without sudo
3. **PATH confusion**: May install to system location not in your user PATH

### Solution: Use Native Installer Instead

**Mac/Linux/Git Bash:**
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**Windows PowerShell:**
```powershell
irm https://claude.ai/install.ps1 | iex
```

This installs to `~/.local/bin/claude` and sets up PATH correctly.

### If Already Installed with sudo

See the [Claude Code Installation Troubleshooting](troubleshooting_claude_install.md) guide for migration steps.

## Advanced PATH Debugging

### Check PATH load order (Mac/Linux)

Add this to your shell config to see when PATH is set:
```bash
echo "Loading ~/.zshrc"
echo "PATH is: $PATH"
```

### Check all PATH locations (Windows)

```powershell
$env:PATH -split ';' | ForEach-Object { $_ }
```

### See which config file is being loaded (Mac)

```bash
echo $SHELL
ls -la ~/.*rc
ls -la ~/.*profile
```

## Tips for Beginners

1. **One terminal type**: Stick with one terminal (Git Bash on Windows, Terminal on Mac) while learning
2. **Restart always**: After any PATH change, close and reopen all terminals
3. **Test incrementally**: Add one directory at a time and test
4. **Use full paths first**: If `claude` doesn't work, try the full path to confirm it's a PATH issue
5. **Document changes**: Keep notes on what you add to PATH and why

## Getting More Help

- Mac PATH: https://mac.install.guide/terminal/path
- Windows PATH: https://www.computerhope.com/issues/ch000549.htm
- Ask in Cursor: Paste your error message and current PATH output
- Claude Code Discord: Share your PATH output for help

## Next Steps

After fixing your PATH:
1. Test that all commands work: `claude`, `node`, `npm`, `python`
2. Verify auto-updates work for Claude Code
3. Document your final PATH configuration
4. Proceed with the main installation guides
