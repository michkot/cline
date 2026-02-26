# Building Cline Extension Locally

This guide explains how to build and install a local version of the Cline VSCode extension with your changes.

## Prerequisites

- [Node.js](https://nodejs.org/) (v20 or higher recommended)
- [git](https://git-scm.com/) with [git-lfs](https://git-lfs.com/)
- [Visual Studio Code](https://code.visualstudio.com/)

## Step 1: Clone and Setup

```bash
# Clone the repository (if you haven't already)
git clone https://github.com/michkot/cline.git
cd cline

# Checkout the branch with your fix
git checkout copilot/prepare-mr-text

# Install dependencies
npm run install:all

# Generate Protocol Buffer files (required before building)
npm run protos
```

## Step 2: Build the Extension

```bash
# Build the extension for production
npm run package
```

This command will:
- Run TypeScript type checks
- Build the webview UI
- Run linter
- Bundle the extension using esbuild in production mode

## Step 3: Package as VSIX (Optional but Recommended)

To create a `.vsix` file that you can install:

```bash
# Install the VS Code Extension packaging tool (if not already installed)
npm install -g @vscode/vsce

# Package the extension
vsce package
```

This will create a `.vsix` file in the root directory (e.g., `cline-3.67.1.vsix`).

## Step 4: Install the Extension

### Option A: Install from VSIX (Recommended)

1. Open VSCode
2. Go to Extensions view (`Ctrl+Shift+X` or `Cmd+Shift+X`)
3. Click the "..." menu at the top of the Extensions panel
4. Select "Install from VSIX..."
5. Navigate to and select the `.vsix` file you created

### Option B: Run in Development Mode

1. Open the project in VSCode:
   ```bash
   code .
   ```

2. Press `F5` (or go to Run → Start Debugging)

3. A new VSCode window will open with the extension loaded

This method is great for testing but won't persist after closing VSCode.

## Verifying Your Changes

After installation, verify that the SHELL environment variable fix is working:

### On Windows:

1. Set the SHELL environment variable (if not already set):
   ```cmd
   setx SHELL "C:\Program Files\Git\bin\bash.exe"
   ```

2. Restart VSCode

3. Open Cline Settings → Terminal Settings → Terminal Execution Mode

4. You should see the Windows-specific help text:
   > "Windows users: Background Exec mode respects the SHELL environment variable, allowing you to use bash from Cygwin, MSYS2, or Git for Windows."

5. Switch to "Background Exec" mode and test that commands run in bash

### On Unix/macOS:

The SHELL variable should work as before with no changes needed.

## Troubleshooting

### "Cannot find module" errors

Make sure you ran:
```bash
npm run install:all
npm run protos
```

### Build fails

Try cleaning and rebuilding:
```bash
# Clean node_modules
rm -rf node_modules webview-ui/node_modules
npm run install:all
npm run protos
npm run package
```

### Extension not loading

- Make sure you uninstall any marketplace version of Cline first
- Try reloading VSCode window (`Ctrl+R` or `Cmd+R`)
- Check the VSCode Developer Console for errors (Help → Toggle Developer Tools)

## Development Workflow

For active development with auto-rebuild:

```bash
# Terminal 1: Watch mode for extension
npm run watch

# Terminal 2: Watch mode for webview (if making UI changes)
cd webview-ui
npm run watch

# Then press F5 in VSCode to start debugging
```

Changes to TypeScript files will be automatically recompiled. Use the reload button in the debug toolbar to restart the extension with your changes.

## Additional Resources

- [CONTRIBUTING.md](CONTRIBUTING.md) - Full contribution guidelines
- [VSCode Extension Development](https://code.visualstudio.com/api) - Official VSCode extension documentation
- [Cline Documentation](https://docs.cline.bot) - User documentation

## What Was Fixed

This build includes the following fixes:

1. ✅ **Terminology corrections** - Proper distinction between environments (Cygwin, MSYS2, Git for Windows) and shells (bash, zsh)

2. ✅ **Complete SHELL support on Windows** - All 3 execution modes now respect the SHELL environment variable:
   - VS Code Terminal Mode
   - Background Execution Mode  
   - Standalone/CLI Mode

3. ✅ **Comprehensive tests** - New test cases verify SHELL env var support on Windows

4. ✅ **Documentation** - Setup guide in terminal quick fixes documentation

5. ✅ **UI guidance** - Windows-specific help text in Terminal Settings

The changes allow Windows users to use bash (from Git for Windows, Cygwin, or MSYS2) by setting the SHELL environment variable, just like on Unix/Linux systems.
