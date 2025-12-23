# KillaDome - COD-Style Rust Server Experience

A complete Call of Duty style game mode plugin system for Rust servers using Oxide/uMod.

## Plugin Files

- **KillaDome.cs** - Main game logic plugin
- **KillaUIv2.cs** - User interface plugin

## Dependencies

### Required Plugins

Both plugins depend on each other:
- **KillaDome.cs** requires **KillaUIv2.cs** for UI functionality
- **KillaUIv2.cs** requires **KillaDome.cs** for game logic and data

### Optional Plugins

- **ImageLibrary** - Recommended for displaying weapon and item images in the UI

## Installation

1. **Install both plugins together:**
   - Copy `KillaDome.cs` to your `oxide/plugins` folder
   - Copy `KillaUIv2.cs` to your `oxide/plugins` folder
   - **Important:** Install both plugins at the same time or reload them together

2. **Install ImageLibrary (Optional but Recommended):**
   - Download ImageLibrary from uMod: https://umod.org/plugins/image-library
   - Copy to your `oxide/plugins` folder

3. **Server Restart/Reload:**
   ```
   oxide.reload KillaDome
   oxide.reload KillaUIv2
   ```

## Plugin Dependencies Explained

### Circular Dependency

These plugins have a **circular dependency**, which means:
- KillaDome calls methods in KillaUIv2 to show UI
- KillaUIv2 calls methods in KillaDome to get game data

This is **safe and intentional** because:
1. Both plugins check if the other is loaded before calling methods
2. Both plugins handle null references gracefully
3. Both plugins provide clear error messages when dependencies are missing

### Load Order

Oxide/uMod will load both plugins, and they will automatically detect each other once both are loaded. There's no specific load order requirement as long as both are present.

## Common Issues

### "KillaUIv2 plugin not found"
**Solution:** Make sure both `KillaDome.cs` AND `KillaUIv2.cs` are in your plugins folder, then reload both plugins.

### "KillaDome plugin not found"
**Solution:** Make sure both `KillaDome.cs` AND `KillaUIv2.cs` are in your plugins folder, then reload both plugins.

### UI not showing
**Cause:** One of the plugins failed to load or the dependency is missing.
**Solution:** 
1. Check the server console for error messages
2. Verify both plugins are loaded: `oxide.plugins`
3. Reload both plugins: `oxide.reload KillaDome` and `oxide.reload KillaUIv2`

## Commands

### Player Commands
- `/kd open` - Open the lobby UI
- `/kd stats` - View your stats
- `/kd help` - Show help

### Admin Commands
- `kd.open` - Open lobby UI (console)
- `kd.start` - Start a match
- `kd.giveskin <steamid> <skinid>` - Give a skin to a player
- `kd.resetprogress <steamid>` - Reset player progress

## Configuration

Configuration file is generated at: `oxide/config/KillaDome.json`

Edit this file to customize:
- Spawn positions
- Starting tokens
- Token rewards
- Tebex integration
- And more...

## Support

For issues or questions:
1. Check the server console for error messages
2. Verify all dependencies are installed
3. Ensure both plugins are loaded together

## Features

- **Lobby System** - Player spawn area with full UI
- **Loadout Editor** - Customize weapons and attachments
- **Weapon Progression** - Level up weapons to unlock attachments
- **Store System** - Buy weapons, skins, and armor with Blood Tokens
- **Match System** - Queue-based matchmaking
- **Stats Tracking** - Track kills, deaths, K/D, and more
- **Settings** - Customizable player preferences

## License

All rights reserved. KillaDome Dev Team.
