# Afterlife Player Editor

**Live player skill management for SCUM dedicated servers.**

Afterlife Player Editor is a Windows desktop administration tool that allows authorized SCUM server owners and administrators to manage online players' skills and experience without stopping the game server or directly modifying its live database.

[Download the latest release](https://github.com/afterlifeteam26-del/AfterlifePlayerEditor/releases/latest) · [Report an issue](https://github.com/afterlifeteam26-del/AfterlifePlayerEditor/issues)

## Features

- Live player selection by name or Steam ID.
- Edit individual or multiple skills, skill levels and experience (XP).
- Sort skills by name, level or numeric experience.
- Max selected skills or all skills to Advanced with a 10,000,000 XP target.
- Batch skill editing with readback verification and cancellation of remaining submissions.
- Multiple saved server profiles and secure SFTP connections.
- Optional password storage using Windows Credential Manager.
- Modern rounded dashboard with charcoal and emerald green styling, customizable themes, accents and fonts.
- Per-server personalization, including display name and logo.
- Dedicated Setup, Diagnostics and Updates pages.
- Automatic GitHub release checks and downloads, with approval before installation.

## Requirements

| Component | Requirement |
| --- | --- |
| Desktop | Windows PC; Windows 11 recommended for native title bar styling |
| Server | Authorized Windows SCUM dedicated server with mod support |
| Connection | SFTP access with appropriate read/write permissions |
| Server dependencies | Compatible UE4SS, SSA Bridge and AfterlifeBridge relay (0.4a or 0.6-preview) |

The packaged Windows installer does not require a separate Python installation. Compiled server companion DLLs are not included in the source kit. Hosting providers and game updates may affect compatibility.

## Installation

1. Open the [GitHub Releases page](https://github.com/afterlifeteam26-del/AfterlifePlayerEditor/releases).
2. Download the latest available stable `AfterlifeSetup_vX.Y.Z.exe` installer.
3. Run the installer and follow the prompts. Installation to Program Files requires administrator approval.
4. Launch Afterlife Player Editor normally after installation.

If only a source archive is available, follow the build instructions below.

## Server setup

Before connecting, install and configure compatible server companions. Back up the server and stop it before installing or replacing server-side mods. Obtain UE4SS and SSA Bridge from their authorized sources and follow their licensing and installation instructions.

The expected relay directory is:

```text
SCUM/Binaries/Win64/Mods/AfterlifeBridge/
```

The relay communicates with SSA Bridge locally. Keep the SSA listener private on `127.0.0.1:27717`; do not expose it to the internet. Enable the supported live player and skill operations in the SSA configuration. Skill writes also require the relay's `allow-writes.txt` marker.

See [Server Setup](docs/SERVER_SETUP.md) for deployment details, and `companion-source/BUILD.txt` for relay build instructions. The desktop Setup page can upload missing companion files from a prepared local folder; it does not compile DLLs, validate existing binaries or provide automatic rollback.

## Connecting to your server

1. Open **Connection settings** and add or select a server profile.
2. Enter the SFTP host, SFTP port, username, password and full remote AfterlifeBridge directory.
3. Save your settings. Optionally save the password using Windows Credential Manager.
4. Connect and review the server host-key fingerprint on first use. Verify it independently with your host before trusting it.
5. Run the compatibility check and refresh the online player list.

Changed host keys are blocked. Investigate unexpected key changes rather than bypassing verification.

## Editing player skills

1. Open **Player editor** and select an online player.
2. Select one or more skills using Ctrl-click or Shift-click.
3. Choose a skill level (None, Basic, Medium or Advanced) and enter the desired XP.
4. Click **Apply selected skills**, or use **Max selected + XP** or **Max all + XP**.
5. Review and confirm the target player and values. Refresh the player's skills to verify the result.

The max buttons target Advanced and 10,000,000 XP; this is not a verified game-wide XP cap. Cancellation stops future submissions, not a write already in progress. There is no automatic rollback. If an operation times out, refresh before attempting another write. Verify persistence after the player reconnects.

## Automatic updates

The editor checks GitHub for newer stable releases on startup. Available updates are downloaded automatically, checked against the release manifest and expected file size, and offered for installation when no server operation is active. Installation requires your approval. The Updates page also supports manual checks.

Desktop updates do not require a SCUM server restart. SHA-256 verification detects file mismatches but does not authenticate the publisher; only install releases from a trusted source.

## Security and privacy

- Passwords are not saved in server profile files. Optional credential storage uses Windows Credential Manager.
- Local settings are stored under `%LOCALAPPDATA%\AfterlifePlayerEditor`.
- The editor does not directly modify the live SCUM SQLite database.
- Restrict SFTP and skill-write access to trusted administrators.
- Never publish credentials, private profiles, host keys or sensitive server logs.
- Review exported diagnostics before sharing them.

## Current limitations

- Attribute editing (Strength, Constitution, Dexterity and Intelligence) is not supported.
- Compatibility diagnostics do not prove write access or persistence.
- Server companion compatibility varies by game build and hosting provider.
- Windows runtime, live acceptance testing and release signing are not fully verified for the v1.3.6 source kit.

## Support

Open a [GitHub issue](https://github.com/afterlifeteam26-del/AfterlifePlayerEditor/issues) with the application version, relevant server companion versions, reproduction steps and sanitized error messages. Never include passwords or tokens.

## Credits and licensing

Afterlife Player Editor uses Python, CustomTkinter, Paramiko, Pillow and Keyring, and interoperates with UE4SS and SSA Bridge. These third-party projects retain their respective licenses. Afterlife Player Editor is an independent community administration tool and is not an official SCUM product. No project license is specified in the reviewed source kit; consult the repository owner for distribution permissions.
