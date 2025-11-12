# ADHD Quest - Desktop Application Build Guide

This guide will help you build ADHD Quest as a standalone desktop application (.exe for Windows, .dmg for Mac, .AppImage for Linux).

## Prerequisites

Before building, make sure you have:
- Node.js installed (v16 or higher)
- npm installed
- Git installed

## First Time Setup

1. **Clone or download the repository**
   ```bash
   git clone <repository-url>
   cd ADQuest
   ```

2. **Install dependencies** (including Electron)
   ```bash
   npm install
   ```

   This will install all required packages including:
   - `electron` - The desktop app framework
   - `electron-builder` - Tool to create installers
   - `concurrently`, `wait-on`, `cross-env` - Development helpers
   - `electron-is-dev` - Detect development vs production

## Development Mode

To test the app as a desktop application during development:

```bash
npm run electron:dev
```

This will:
1. Start the React development server
2. Wait for it to be ready
3. Launch the Electron window
4. Enable hot-reloading for quick development

**Note:** The DevTools will open automatically in development mode.

## Building for Distribution

### Build for Windows (.exe installer)

```bash
npm run electron:build:win
```

This creates:
- An installer in `dist/ADHD Quest Setup <version>.exe`
- Users can double-click to install
- Creates desktop shortcut and start menu entry

**Installer features:**
- Choose installation directory
- Create desktop shortcut
- Add to Start Menu
- ~150-200MB size

### Build for macOS (.dmg)

```bash
npm run electron:build:mac
```

Creates a `.dmg` file in the `dist` folder that users can drag to Applications.

**Note:** Building for Mac requires macOS. For code signing, you'll need an Apple Developer account.

### Build for Linux (.AppImage and .deb)

```bash
npm run electron:build:linux
```

Creates:
- `.AppImage` - Portable, runs anywhere
- `.deb` - Installable package for Debian/Ubuntu

### Build for All Platforms

```bash
npm run electron:build
```

This builds for your current platform only. To build for multiple platforms, you need to run on each respective OS or use CI/CD.

## What Gets Built?

The build process:
1. Compiles your React app (`npm run build`)
2. Packages it with Electron
3. Creates platform-specific installers
4. Output goes to the `dist/` folder

## Distribution

### Option 1: GitHub Releases (Recommended)

1. Create a new release on GitHub
2. Upload the installer files from `dist/` folder
3. Users download and install

Example for Windows:
- Upload: `ADHD Quest Setup 0.1.0.exe`
- Users download, double-click, install!

### Option 2: Direct Download

Host the installer files on any file hosting service:
- Google Drive
- Dropbox
- Your own website

### Option 3: Auto-Updates (Advanced)

Configure electron-builder with update server for automatic updates. See: https://www.electron.build/auto-update

## File Sizes

Typical installer sizes:
- **Windows**: ~150-180 MB
- **macOS**: ~160-190 MB
- **Linux AppImage**: ~140-170 MB

Why so large? The installer includes:
- Your React app (~5-10 MB)
- Electron/Chromium (~140 MB)
- Node.js runtime (~30 MB)

## Troubleshooting

### Build fails with "Cannot find module 'electron'"

Run:
```bash
npm install
```

### "Error: ENOENT: no such file or directory, open 'build/index.html'"

You need to build the React app first:
```bash
npm run build
npm run electron:build:win
```

Or use the combined command that does this automatically:
```bash
npm run electron:build:win
```

### Installer is too large

This is normal! Electron bundles a full browser. Consider:
- Using Tauri instead (creates ~10-15 MB installers)
- Or host as a web app instead

### Icon not showing

Make sure you have icons in the `public` folder:
- Windows: `public/favicon.ico` (256x256 or multi-size .ico)
- Mac: `public/favicon.icns` (512x512 .icns format)
- Linux: `public/favicon.png` (512x512 .png)

To create .icns for Mac:
```bash
# On Mac:
mkdir icon.iconset
sips -z 512 512 icon.png --out icon.iconset/icon_512x512.png
iconutil -c icns icon.iconset
```

## Configuration Files

### `electron.js`
Main Electron process - creates the app window and manages the application lifecycle.

### `package.json` - Key sections:
- `"main": "electron.js"` - Entry point
- `"homepage": "./"` - Use relative paths
- `"build"` - electron-builder configuration

## Development Tips

1. **Quick testing**: Use `npm run electron:dev` for fast iteration
2. **Production testing**: Build once with `npm run electron:build:win` and test the installer
3. **Debugging**: Check Console in DevTools (opens automatically in dev mode)
4. **Clean builds**: Delete `dist/` and `build/` folders if you encounter issues

## User Experience

After installation, users will:
1. Find "ADHD Quest" in their Start Menu / Applications
2. Double-click to launch
3. App opens in a native window (not browser)
4. All data saves locally using localStorage
5. Works completely offline

## Next Steps

After building:
1. Test the installer on a clean machine
2. Create a GitHub Release
3. Share the download link
4. Consider adding auto-updates for v2.0

## Additional Resources

- [Electron Documentation](https://www.electronjs.org/docs)
- [electron-builder Docs](https://www.electron.build/)
- [Packaging Tutorial](https://www.electronjs.org/docs/latest/tutorial/tutorial-packaging)

## Need Help?

Common issues and solutions in the Troubleshooting section above. For other issues, check:
- Electron Builder issues: https://github.com/electron-userland/electron-builder/issues
- Electron issues: https://github.com/electron/electron/issues
