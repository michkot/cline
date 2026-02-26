# Quick Build Guide

## TL;DR - Fast Build

```bash
# 1. Setup (one-time)
git clone https://github.com/michkot/cline.git
cd cline
git checkout copilot/prepare-mr-text
npm run install:all
npm run protos

# 2. Build
npm run package

# 3. Package and Install
npx @vscode/vsce package
# Then in VSCode: Extensions → "..." → Install from VSIX → select the .vsix file
```

## Just Want to Test in Dev Mode?

```bash
# In the cline directory:
code .
# Then press F5 in VSCode
```

A new VSCode window opens with the extension loaded. Perfect for quick testing!

## Common Commands

| Command | Purpose |
|---------|---------|
| `npm run install:all` | Install all dependencies |
| `npm run protos` | Generate Protocol Buffer files (required once) |
| `npm run package` | Build production bundle |
| `npm run watch` | Build + watch for changes |
| `npm test` | Run tests |
| `npx @vscode/vsce package` | Create .vsix file |

## What's in This Build?

✅ SHELL environment variable now respected on Windows (all execution modes)  
✅ Use bash from Git for Windows, Cygwin, or MSYS2  
✅ Proper terminology (environments vs shells)  
✅ Documentation and UI guidance added

## Need More Details?

See [BUILD_LOCAL.md](BUILD_LOCAL.md) for the complete guide with troubleshooting.
