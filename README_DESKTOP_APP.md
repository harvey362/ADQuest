# ADHD Quest - Desktop App Quick Start

## For End Users (Downloading the App)

### Windows

1. Go to the Releases page
2. Download `ADHD Quest Setup.exe`
3. Double-click the installer
4. Follow the installation wizard
5. Launch from Start Menu or Desktop shortcut

**No Node.js, npm, or technical setup required!**

### macOS

1. Go to the Releases page
2. Download `ADHD Quest.dmg`
3. Open the DMG file
4. Drag ADHD Quest to Applications
5. Launch from Applications folder

### Linux

1. Go to the Releases page
2. Download `ADHD Quest.AppImage`
3. Make it executable: `chmod +x ADHD-Quest*.AppImage`
4. Double-click to run (no installation needed)

## For Developers (Building the App)

See [ELECTRON_BUILD_GUIDE.md](ELECTRON_BUILD_GUIDE.md) for complete build instructions.

### Quick Build Commands

```bash
# Install dependencies (first time only)
npm install

# Build Windows installer
npm run electron:build:win

# Build for Mac
npm run electron:build:mac

# Build for Linux
npm run electron:build:linux

# Test in development mode
npm run electron:dev
```

## What Changed?

Your ADHD Quest app is now a **standalone desktop application**:

### ✅ What Works
- Opens as a native Windows/Mac/Linux application
- No browser needed
- Works completely offline
- All data stored locally
- Faster startup
- Desktop icon and shortcuts
- Installs like any normal program

### 📦 File Structure (New)
- `electron.js` - Main Electron process
- `package.json` - Updated with Electron scripts
- `ELECTRON_BUILD_GUIDE.md` - Complete build documentation

## Running the App

### As Desktop App (Production)
Double-click the installed application icon.

### As Web App (Still works!)
```bash
npm start
```
Then open http://localhost:3000 in your browser.

### In Electron Development Mode
```bash
npm run electron:dev
```

## Data Storage

Your tasks, XP, and settings are stored locally in:
- **Windows**: `%APPDATA%\adhd-productivity-app\`
- **macOS**: `~/Library/Application Support/adhd-productivity-app/`
- **Linux**: `~/.config/adhd-productivity-app/`

This uses the same localStorage API, but Electron stores it persistently.

## Benefits of Desktop Version

1. **No Installation Complexity**: Users just download and install like any normal program
2. **Offline First**: No internet required after download
3. **Better Performance**: Direct system integration
4. **Professional Feel**: Appears in Application list, has proper icon
5. **Data Privacy**: Everything stays on the user's computer
6. **Easy Updates**: Can add auto-update feature later

## Distribution Options

### Option 1: GitHub Releases (Free)
1. Create a release on your GitHub repository
2. Upload the built installers
3. Share the release page URL

### Option 2: Your Own Website
Host the installer files and provide download links.

### Option 3: Microsoft Store / Mac App Store (Paid)
Requires developer account but provides automatic updates and discoverability.

## FAQs

**Q: Can I still run it in the browser?**
A: Yes! The web version (`npm start`) still works perfectly.

**Q: Why is the installer so large (150+ MB)?**
A: It includes everything needed to run: your app + Chromium + Node.js. Users don't need to install anything else.

**Q: Can users install it without admin rights?**
A: Yes, the installer can be configured for per-user installation.

**Q: Will my existing data transfer?**
A: The desktop app uses separate storage. Data doesn't automatically transfer from browser localStorage.

**Q: How do I update the app later?**
A: Build a new version, increment the version in package.json, and redistribute. Or add auto-update feature.

## Support

For build issues, see [ELECTRON_BUILD_GUIDE.md](ELECTRON_BUILD_GUIDE.md)
For app features, see main [README.md](README.md)
