# Counter-Strike 2 Pterodactyl Egg (Modified by saka)

A Pterodactyl egg for running Counter-Strike 2 servers using Valve's Steam Runtime 3 platform. This egg is based on the original CS2 egg but includes modifications for improved functionality.

## Features

- ✅ **Steam Runtime 3 Support** - Uses Valve's latest runtime environment
- ✅ **VAC Protection** - Configurable Valve Anti-Cheat support
- ✅ **RCON Support** - Remote console access for server administration
- ✅ **SourceTV** - Built-in spectator support
- ✅ **Game Mode Flexibility** - Support for all CS2 game modes
- ✅ **Conditional Password** - Server password only applied when set
- ✅ **Auto-Updates** - Configurable automatic server updates

## Docker Images

| Image | Description |
|-------|-------------|
| `ghcr.io/1zc/steamrt3-pterodactyl:latest` | Stable release (recommended) |
| `ghcr.io/1zc/steamrt3-pterodactyl:beta-latest` | Public beta version |
| `ghcr.io/1zc/steamrt3-pterodactyl:dev` | Development version |
| `ghcr.io/1zc/steamrt3-pterodactyl:beta-dev` | Beta development version |

## Installation

1. Download the `cs2-sakoa.json` egg file
2. In your Pterodactyl admin panel, navigate to **Nests** → **Import Egg**
3. Upload the JSON file and configure as needed
4. Create a new server using this egg

## Configuration Variables

### Server Settings

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| **Map** | Default map for the server | `de_dust2` | ✅ |
| **Max Players** | Maximum number of players | `64` | ✅ |
| **Server Name** | Name displayed in server browser | `A Pterodactyl hosted CS2 Server` | ✅ |
| **Server Password** | Password to join server (optional) | _(empty)_ | ❌ |

### Game Mode Configuration

| Variable | Description | Default |
|----------|-------------|---------|
| **Game Mode** | Game mode number (see table below) | `1` |
| **Game Type** | Game type number (see table below) | `0` |
| **Game Alias** | Predefined game mode alias | _(empty)_ |

#### Game Mode Reference

| Mode | game_mode | game_type | Description |
|------|-----------|-----------|-------------|
| Competitive | 1 | 0 | Standard competitive matches |
| Wingman | 2 | 0 | 2v2 competitive matches |
| Casual | 0 | 0 | Casual gameplay |
| Deathmatch | 2 | 1 | Free-for-all deathmatch |
| Arms Race | 0 | 1 | Progressive weapon gameplay |
| Custom | 0 | 3 | Custom game modes |

**Note:** Game Alias will override manual game_mode and game_type settings. Valid aliases: `competitive`, `wingman`, `deathmatch`, `custom`, `casual`

### Network & Security

| Variable | Description | Default |
|----------|-------------|---------|
| **SourceTV Port** | Port for spectator connections | `27020` |
| **Enable VAC** | Valve Anti-Cheat protection | `1` (enabled) |
| **Enable RCON** | Remote console access | `0` (disabled) |
| **RCON Password** | Password for RCON access | _(required if RCON enabled)_ |

### Steam Integration

| Variable | Description | Default |
|----------|-------------|---------|
| **Game Server Login Token (GSLT)** | Steam token for public listing | _(empty)_ |
| **Validate Install** | Verify game files on startup | `0` (disabled) |
| **Disable Updates** | Prevent automatic updates | `0` (updates enabled) |

## Port Requirements

| Port | Protocol | Purpose | Configurable |
|------|----------|---------|--------------|
| Primary | UDP | Game server | ✅ (via Pterodactyl) |
| TV Port | UDP | SourceTV spectating | ✅ (default: 27020) |

## Key Modifications

This modified egg includes the following improvements:

1. **Conditional Password**: The `+sv_password` parameter is only added to the startup command when a password is actually set, preventing issues with empty password values.

2. **Enhanced Conditional Logic**: Uses robust shell scripting for parameter inclusion based on configuration.

## Getting a Game Server Login Token (GSLT)

1. Visit [Steam Game Server Account Management](https://steamcommunity.com/dev/managegameservers)
2. Log in with your Steam account
3. Create a new game server account
4. Use App ID `730` for Counter-Strike 2
5. Copy the generated token to the GSLT field

## Troubleshooting

### Common Issues

**Server not appearing in browser:**
- Ensure GSLT is properly configured
- Check that VAC is enabled for public servers
- Verify firewall settings allow the server port

**Players cannot connect:**
- Confirm server password is correctly set (or empty)
- Check that the server port is properly forwarded
- Verify max players setting

**RCON not working:**
- Enable RCON in server settings
- Set a strong RCON password
- Use the correct port for RCON connections

### Log Files

Server logs are available through the Pterodactyl console. Look for:
- `Connection to Steam servers successful` - Indicates successful startup
- VAC status messages
- Player connection/disconnection events

## Support

For issues specific to this egg modification, please check the repository issues. For general CS2 server support, refer to:
- [Valve Developer Wiki](https://developer.valvesoftware.com/wiki/Counter-Strike_2/Dedicated_Servers)
- [CS2 Server Documentation](https://developer.valvesoftware.com/wiki/Counter-Strike_2)

## Credits

- **Original Egg**: infra@gflclan.com
- **Modifications**: saka
- **Base Image**: [1zc/steamrt3-pterodactyl](https://github.com/1zc/steamrt3-pterodactyl)
