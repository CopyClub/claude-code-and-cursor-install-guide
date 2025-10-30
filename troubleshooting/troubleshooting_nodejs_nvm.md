# Troubleshooting Node.js and nvm Installation

> Solutions for installing Node.js, deciding whether to use nvm, and common issues.

## Why Install Node.js for Claude Code?

Node.js and npm (Node Package Manager) are required if you're installing Claude Code via npm. However, there's also a native installer that doesn't require Node.js.

### Two Installation Paths

1. **Native installer (Recommended)**: No Node.js required
   ```bash
   curl -fsSL https://claude.ai/install.sh | bash
   ```

2. **npm installer**: Requires Node.js and npm
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```

Even if you use the native installer, Node.js is useful for many development tasks that Claude Code might help you with.

## Should You Use nvm (Node Version Manager)?

### What is nvm?

nvm is a tool for managing multiple Node.js versions on your computer, similar to how pyenv manages Python versions.

### For Non-Developers: Simple Answer

**If you're new to development and just want Claude Code:**
- **No, you don't need nvm initially**
- Install Node.js directly for simplicity
- You can always add nvm later if needed

**If you plan to do regular development work:**
- **Yes, nvm is recommended**
- Easier version management
- Avoid permission issues
- Professional best practice

### Pros of Using nvm

1. **No permission issues**: Installs in your home directory
2. **Multiple versions**: Switch between Node versions easily
3. **No sudo required**: Cleaner installation
4. **Project-specific versions**: Different projects can use different Node versions
5. **AI tools understand it**: Claude and other AI assistants know about nvm

### Cons of Using nvm

1. **Slightly more complex**: Extra commands to learn
2. **Path complexity**: Adds another layer to PATH configuration
3. **Not needed for simple use**: Overkill if you just want one Node version

## Installing Node.js Without nvm (Simple Method)

### Mac

**Option 1: Official Installer (Easiest)**
1. Visit https://nodejs.org
2. Download the LTS (Long Term Support) version
3. Run the installer
4. Follow the installation wizard
5. Restart Terminal

**Option 2: Homebrew**
```bash
# Requires Homebrew to be installed first
brew install node

# Verify installation
node --version
npm --version
```

### Windows

1. Visit https://nodejs.org
2. Download the LTS (Long Term Support) installer
3. Run the .msi installer
4. **IMPORTANT**: Check "Automatically install the necessary tools" during setup
5. Follow the installation wizard
6. Restart Git Bash or PowerShell

**Verify Installation:**
```bash
node --version
npm --version
```

## Installing Node.js With nvm (Recommended Method)

### Mac Installation

```bash
# Install nvm via curl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Or via wget
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Add to shell configuration (usually automatic, but verify)
echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.zshrc
echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.zshrc

# Reload shell configuration
source ~/.zshrc

# Install latest LTS Node.js
nvm install --lts

# Set it as default
nvm use --lts
nvm alias default node

# Verify
node --version
npm --version
```

### Windows Installation

**Important: Uninstall any existing Node.js installations first**

1. Go to Settings > Apps > Installed apps
2. Uninstall Node.js if present
3. Restart your computer

**Install nvm-windows:**

1. Visit: https://github.com/coreybutler/nvm-windows/releases
2. Download `nvm-setup.zip` from the latest release
3. Extract and run `nvm-setup.exe`
4. During installation:
   - **Change the symlink path to avoid spaces**: Use `C:\nvm\nodejs` instead of `C:\Program Files\nodejs`
5. Complete the installation
6. Restart Git Bash or PowerShell

**Install Node.js with nvm:**

```bash
# List available Node versions
nvm list available

# Install latest LTS version (e.g., 20.10.0)
nvm install 20.10.0

# Use that version
nvm use 20.10.0

# Verify
node --version
npm --version
```

## Common Issues

### Issue: nvm command not found (Mac)

**Cause**: Shell configuration not loaded properly.

**Solution**:
```bash
# Check if nvm is sourced in your shell config
cat ~/.zshrc | grep nvm

# If missing, add these lines
echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.zshrc
echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.zshrc
echo '[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"' >> ~/.zshrc

# Reload
source ~/.zshrc

# Or directly source nvm
source ~/.nvm/nvm.sh
```

### Issue: nvm command not found (Windows)

**Cause**: Installation path not in PATH or installation failed.

**Solution**:
1. Check Windows Environment Variables for nvm paths:
   - `C:\Users\[YourName]\AppData\Roaming\nvm`
   - `C:\nvm` (or wherever you installed it)
2. Restart all terminal windows
3. Restart computer if still not working
4. Try running command prompt as Administrator

### Issue: node/npm commands not found after installing nvm

**Cause**: No Node version installed or activated.

**Solution**:
```bash
# List installed versions
nvm list

# If empty, install Node
nvm install --lts

# Activate it
nvm use --lts

# Set as default (Mac/Linux)
nvm alias default node

# Verify
node --version
```

### Issue: Different Node versions in different terminals

**Cause**: nvm version not set as default.

**Solution**:
```bash
# Mac/Linux
nvm alias default 20.10.0

# Windows - set the default in system PATH
# The symlink should handle this automatically
```

### Issue: npm install -g fails with EACCES permission errors

**Cause**: Improper Node.js installation or ownership issues.

**Solution with nvm**:
```bash
# nvm should handle this automatically
# Verify nvm is managing Node
which node  # Should show path in .nvm directory
```

**Solution without nvm** (Mac):
```bash
# Fix npm permissions
mkdir -p ~/.npm-global
npm config set prefix '~/.npm-global'

# Add to PATH in ~/.zshrc
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.zshrc
source ~/.zshrc
```

### Issue: WSL shows Windows Node/npm instead of Linux version

**Cause**: Windows PATH imported into WSL taking priority.

**Solution**: See [Claude Code Troubleshooting - WSL nvm conflicts](troubleshooting_claude_install.md#windows-installation-issues-errors-in-wsl)

### Issue: Switching Node versions breaks npm

**Cause**: npm was installed globally with a different Node version.

**Solution**:
```bash
# Reinstall npm for current Node version
nvm install-latest-npm

# Or reinstall the Node version
nvm uninstall 20.10.0
nvm install 20.10.0
```

### Issue: nvm is slow (Windows)

**Cause**: nvm-windows can be slower than Linux/Mac nvm.

**Solutions**:
1. Use PowerShell instead of Git Bash (slightly faster)
2. Set a default Node version to avoid repeated switching
3. Consider using the official Node.js installer if you only need one version

## Using nvm: Common Commands

### Installing Node Versions

```bash
# Install latest LTS
nvm install --lts

# Install specific version
nvm install 18.17.0

# Install latest version (not LTS)
nvm install node
```

### Switching Versions

```bash
# List installed versions
nvm list

# Use specific version
nvm use 18.17.0

# Use latest LTS
nvm use --lts
```

### Setting Defaults

```bash
# Set default version (Mac/Linux)
nvm alias default 18.17.0

# Set default to LTS
nvm alias default --lts
```

### Uninstalling Versions

```bash
# Uninstall a specific version
nvm uninstall 16.14.0
```

## Deciding on nvm: Decision Matrix

| Scenario | Recommendation |
|----------|----------------|
| Just want Claude Code working quickly | **Don't use nvm** - use native Claude Code installer |
| Planning to do web development | **Use nvm** - you'll need version flexibility |
| Already installed Node without nvm | **Keep it** - only switch if you have issues |
| Having permission issues with npm | **Switch to nvm** - solves most permission problems |
| Working on multiple projects | **Use nvm** - different projects need different versions |
| Complete beginner, first time coding | **Don't use nvm** - keep it simple initially |

## Verifying Your Node.js Setup

After installation (with or without nvm), verify everything works:

```bash
# Check Node version
node --version

# Check npm version
npm --version

# Check where they're installed
which node
which npm

# For nvm users, check nvm is managing Node
nvm current

# Test Node works
node -e "console.log('Hello from Node.js!')"

# Test npm works
npm --version
```

## Best Practices

1. **Use LTS versions**: More stable than latest versions
2. **Update regularly**: Keep Node and npm up to date
3. **Document your version**: Remember which Node version you're using
4. **One installation method**: Don't mix nvm with system Node.js
5. **Restart terminals**: After any Node/nvm installation

## Claude Code Specific Considerations

If you're using Claude Code:

1. **Native installer is recommended**: Avoids Node.js issues entirely
2. **If using npm installer**: nvm helps avoid permission issues
3. **AI understands nvm**: Claude can help you with nvm commands
4. **No sudo**: Never use `sudo npm install` - causes auto-update issues

## Getting More Help

- Official Node.js docs: https://nodejs.org/docs
- nvm GitHub: https://github.com/nvm-sh/nvm
- nvm-windows GitHub: https://github.com/coreybutler/nvm-windows
- npm documentation: https://docs.npmjs.com
- Ask in Cursor with your error messages

## Next Steps

After successfully installing Node.js:
1. Test node and npm commands work
2. If using npm, install Claude Code: `npm install -g @anthropic-ai/claude-code`
3. Or use the native installer for Claude Code instead
4. Configure your PATH if needed (see [PATH Troubleshooting](troubleshooting_path_config.md))
5. Verify Claude Code works: `claude --version`
