# Troubleshooting Cursor Installation

> Solutions for common issues when installing Cursor IDE on Mac and Windows.

## What is Cursor?

Cursor is an AI-powered IDE built on VS Code that helps you write, modify, and understand code using natural language instructions. It's available for Windows, macOS, and Linux.

## System Requirements

Before installing Cursor, ensure your system meets these requirements:

- Windows, macOS 10.15 (or newer), or Ubuntu 20.04 (or newer Linux distribution)
- At least 4 GB RAM
- 2 GB available disk space

## Installation Steps by Platform

### Windows

1. Visit the official Cursor website
2. Click the "Windows" button to download
3. Choose the correct architecture:
   - Most Windows systems use **x64**
   - ARM-based devices should choose **arm64**
4. Run the installer and follow the setup wizard

### macOS

1. Visit the official Cursor website
2. Download the .dmg file for Mac
3. Double-click the .dmg file to mount it
4. Drag the Cursor AI application icon to the Applications folder
5. Double-click the Cursor AI application in Applications to launch it

### Linux

1. Visit the official Cursor website
2. Click the Linux button to download the AppImage file
3. Choose the appropriate architecture:
   - **x86_64** for 64-bit systems
   - **aarch64** for ARM-based systems
4. Make the AppImage executable: `chmod +x Cursor-*.AppImage`
5. Run the AppImage file

## Common Issues

### Mac: "Cursor.app" cannot be opened because the developer cannot be verified

This is a macOS security feature called Gatekeeper.

**Solution:**
1. Go to System Preferences > Security & Privacy
2. Click the "Open Anyway" button next to the Cursor message
3. Alternatively, right-click the Cursor app and select "Open"

### Windows: "Windows protected your PC" SmartScreen warning

This warning appears for newly downloaded applications.

**Solution:**
1. Click "More info"
2. Click "Run anyway"
3. The installer will proceed normally

### Linux: AppImage won't run

**Solution:**
1. Make sure you've made the file executable:
   ```bash
   chmod +x Cursor-*.AppImage
   ```
2. If you get a FUSE error, install FUSE:
   ```bash
   # Ubuntu/Debian
   sudo apt install libfuse2

   # Fedora
   sudo dnf install fuse
   ```

### Cursor opens but doesn't connect to AI

**Solution:**
1. Check your internet connection
2. Sign in or create a Cursor account
3. Verify your subscription status
4. Try restarting Cursor

### High memory or CPU usage

Cursor is resource-intensive, especially with large codebases.

**Solution:**
1. Close unnecessary tabs and windows
2. Restart Cursor periodically
3. Check that you have at least 4GB RAM available
4. Consider upgrading your system if performance is consistently poor

## Why Install Cursor Before Claude Code?

When helping non-developers install Claude Code, it's recommended to install Cursor first because:

1. **Built-in terminal troubleshooting**: Cursor's AI can help you troubleshoot terminal commands and error messages
2. **Familiar environment**: If you encounter issues during Claude Code installation, you can paste error messages into Cursor for help
3. **Development environment**: Cursor provides a complete IDE for working with code that Claude Code generates

## Getting More Help

- Official Cursor documentation: Visit the Cursor website for tutorials
- Cursor community forums: Connect with other users
- GitHub issues: Report bugs at the Cursor GitHub repository

## Next Steps

After successfully installing Cursor, you can proceed with:
- Installing additional development tools (Git, Node.js, Python)
- Setting up Claude Code
- Configuring your development environment
