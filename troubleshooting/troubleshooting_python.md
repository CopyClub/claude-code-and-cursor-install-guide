# Troubleshooting Python Installation

> Solutions for common Python installation issues, including pyenv vs global installation, python vs python3 commands, and best practices for working with Claude Code.

## Why Install Python for Claude Code?

While Python is not required for Claude Code itself, it's highly recommended because:

1. **Business process automation**: Many Claude Code workflows involve Python scripts
2. **Data analysis**: Python is commonly used for data processing tasks
3. **Package ecosystem**: Access to pip and thousands of Python packages
4. **AI expectations**: Claude and other AI tools frequently generate Python code

## The python vs python3 Problem on Mac

One of the most frustrating issues on Mac is the difference between `python` and `python3` commands.

### Why This Happens

- **macOS built-in Python 2**: Older Macs come with Python 2.7 as `python`
- **Python 3 installations**: Install as `python3` to avoid conflicts
- **AI tools assume `python`**: Most AI assistants generate code using `python`, not `python3`
- **Constant errors**: You have to manually change `python` to `python3` every time

### Checking Your Current Setup

```bash
python --version    # Might show Python 2.7 or "command not found"
python3 --version   # Should show Python 3.x
which python        # Shows path to python
which python3       # Shows path to python3
```

### Solution 1: Create an alias (Quick but not ideal)

Add to `~/.zshrc`:
```bash
alias python=python3
alias pip=pip3
```

**Pros**: Quick and easy
**Cons**: Only works in your shell, not in scripts or apps

### Solution 2: Use pyenv to set a global default (Recommended)

See the pyenv installation section below. This is the cleanest solution.

## Global Installation vs pyenv

### Global Installation (Simple Approach)

**What it means**: Install Python directly on your system, available everywhere.

**Pros**:
- Simple and straightforward
- No version management complexity
- Works immediately with all tools

**Cons**:
- Only one Python version at a time (without complex workarounds)
- May get VS Code warnings about global installations
- Harder to match project-specific Python versions
- Can conflict with system Python on Mac

### pyenv Installation (Recommended for 2025)

**What it means**: Install pyenv (Python version manager) to manage multiple Python versions.

**Pros**:
- Install and switch between multiple Python versions
- Set a global default Python version
- Set project-specific Python versions
- Clean isolation from system Python
- No permission issues
- Can set `python` (not just `python3`) as the default command

**Cons**:
- Slightly more complex initial setup
- Need to understand pyenv commands
- Can confuse beginners initially

### Recommended Approach for Claude Code Users

**Use pyenv** for these reasons:

1. Sets `python` command to Python 3 (fixes the python vs python3 issue)
2. No `sudo` required (avoids permission problems)
3. Clean version management
4. Professional development practice
5. VS Code and other tools understand pyenv
6. AI tools can use `python` commands without modification

## Installing Python with pyenv

### Mac Installation

#### Prerequisites

Install Homebrew and XCode Command Line Tools first (see [Homebrew Troubleshooting](troubleshooting_homebrew.md) and [XCode Troubleshooting](troubleshooting_xcode.md)).

#### Install pyenv

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

#### Install Python with pyenv

```bash
# See available Python versions
pyenv install --list

# Install the latest Python 3 (e.g., 3.12.0)
pyenv install 3.12.0

# Set it as your global default
pyenv global 3.12.0

# Verify
python --version  # Should show Python 3.12.0 (no need for python3!)
which python      # Should show ~/.pyenv/shims/python
```

### Windows Installation

#### Option 1: Official Python Installer (Simpler)

1. Download from https://www.python.org/downloads/
2. Run the installer
3. **IMPORTANT**: Check "Add Python to PATH"
4. Click "Install Now"
5. Restart Git Bash or PowerShell

#### Option 2: pyenv-win (Advanced)

```powershell
# Install with PowerShell
Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"

# Restart PowerShell, then install Python
pyenv install 3.12.0
pyenv global 3.12.0
```

## Common Python Installation Issues

### Issue: 'python' command not found (Mac)

**Solution with pyenv**:
```bash
# Check pyenv status
pyenv versions

# Set global version
pyenv global 3.12.0

# Verify shell initialization
echo $PATH | grep pyenv
```

**Solution without pyenv**:
```bash
# Create symlink (requires admin)
sudo ln -s $(which python3) /usr/local/bin/python
```

### Issue: 'python' command not found (Windows)

**Solution**:
1. Reinstall Python with "Add to PATH" checked
2. Or manually add Python to PATH (see [PATH Troubleshooting](troubleshooting_path_config.md))
3. Typical paths:
   - `C:\Users\[YourName]\AppData\Local\Programs\Python\Python312`
   - `C:\Users\[YourName]\AppData\Local\Programs\Python\Python312\Scripts`

### Issue: VS Code warns about global Python installation

**Cause**: VS Code recommends using virtual environments for projects.

**Solution**:
1. **Use pyenv**: VS Code recognizes pyenv installations
2. **Use virtual environments for projects**: Create venvs for each project
3. **Ignore the warning**: If you understand the tradeoff, you can dismiss it

### Issue: pip installation fails with permission errors

**Cause**: Trying to install packages globally without proper permissions.

**Solution**:
```bash
# Don't use sudo! Use user installation instead:
pip install --user package-name

# Or use virtual environments:
python -m venv myproject_env
source myproject_env/bin/activate  # Mac/Linux
myproject_env\Scripts\activate     # Windows
pip install package-name
```

### Issue: Multiple Python versions conflict

**Solution with pyenv**:
```bash
# List installed versions
pyenv versions

# Switch global version
pyenv global 3.12.0

# Switch version for current directory only
pyenv local 3.11.0
```

**Solution without pyenv**:
- Remove older Python installations
- Keep only one version
- Use full paths when needed: `/usr/local/bin/python3.12`

### Issue: pyenv installation fails on Mac (build errors)

**Cause**: Missing development dependencies.

**Solution**:
```bash
# Install required build dependencies
brew install openssl readline sqlite3 xz zlib

# Try installation again
pyenv install 3.12.0
```

### Issue: After pyenv install, python command still doesn't work

**Cause**: Shell configuration not loaded or incorrect.

**Solution**:
```bash
# Verify shell configuration
cat ~/.zshrc | grep pyenv

# Should see these lines:
# export PYENV_ROOT="$HOME/.pyenv"
# export PATH="$PYENV_ROOT/bin:$PATH"
# eval "$(pyenv init -)"

# If missing, add them
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc

# Reload configuration
source ~/.zshrc

# Set global Python
pyenv global 3.12.0
```

## Understanding Virtual Environments

Even with pyenv, you might want virtual environments for projects.

### What are Virtual Environments?

A virtual environment is an isolated Python environment for a specific project, with its own packages.

### When to Use Virtual Environments

- **Per-project dependencies**: Each project can have different package versions
- **Avoid conflicts**: Project A needs package v1, Project B needs package v2
- **Clean testing**: Test installations without affecting global Python

### Creating a Virtual Environment

```bash
# Navigate to your project directory
cd my_project

# Create virtual environment
python -m venv venv

# Activate it
source venv/bin/activate  # Mac/Linux/Git Bash
venv\Scripts\activate     # Windows PowerShell

# Now pip installations are isolated to this project
pip install requests

# Deactivate when done
deactivate
```

## Verifying Your Python Setup

After installation, run these checks:

```bash
# Check Python version
python --version

# Verify it's Python 3.x
python --version | grep "Python 3"

# Check pip
pip --version

# Verify command locations
which python
which pip

# Test Python works
python -c "print('Hello from Python!')"

# Check installed packages
pip list
```

## Best Practices for Python with Claude Code

1. **Use pyenv**: Cleanest solution for the python vs python3 issue
2. **Set a global default**: So AI tools can use `python` command
3. **Use venv for projects**: Create isolated environments for specific projects
4. **Keep pip updated**: `pip install --upgrade pip`
5. **Document your setup**: Remember which Python version you're using
6. **Restart terminals**: After any Python installation or PATH changes

## Alternative: UV (Emerging Tool)

A new Python version and package manager called UV is gaining popularity in 2025:

```bash
# Install UV (Mac/Linux)
curl -LsSf https://astral.sh/uv/install.sh | sh

# UV can bootstrap Python itself
uv python install 3.12.0

# And manage virtual environments
uv venv
```

UV is faster and more modern, but pyenv is more established and documented.

## Getting More Help

- Official Python documentation: https://docs.python.org
- pyenv GitHub: https://github.com/pyenv/pyenv
- Real Python tutorials: https://realpython.com
- Python Discord communities
- Ask in Cursor with your error messages

## Next Steps

After successfully installing Python:
1. Verify `python` command works (not just `python3`)
2. Install common packages: `pip install requests pandas numpy`
3. Test with Claude Code by asking it to generate a Python script
4. Set up virtual environments for projects as needed
5. Consider configuring VS Code Python extension
