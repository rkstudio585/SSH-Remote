# SSH Commander

A feature-rich SSH client for Termux designed for efficient remote server management.

This script provides a command-line interface to manage SSH connection profiles, execute commands, run macros, and engage in interactive sessions, all within the Termux environment.

## Features

- **Connection Profiles**: Securely save and manage SSH connection details (host, user, port, auth type).
- **Encrypted Password Storage**: Passwords are encrypted using the `cryptography` library.
- **Dual Authentication**: Supports both password and public key authentication.
- **Command Execution**: Run single commands directly from the command line.
- **Macro System**: Define and run sequences of commands (macros) on your profiles.
- **Interactive Shell**: Open an interactive SSH session for manual command entry.
- **Session Logging**: Automatically saves session output to `~/ssh_logs/`.
- **Color-Coded Output**: Differentiates between commands, output, and errors for better readability.
- **Termux Integration**: Works with Termux's file system and OpenSSH keys.

## Prerequisites

Before using SSH Commander, ensure you have the necessary packages installed in Termux:

```bash
pkg install openssh python
pip install paramiko cryptography
```

## Installation

1. Clone this repository or download the `ssh-commander` script.
2. Make the script executable:
   ```bash
   chmod +x ssh-commander
   ```
3. (Optional) Move the script to a directory in your PATH for global access:
   ```bash
   mv ssh-commander ~/../usr/bin/
   ```

## Usage

SSH Commander uses a command-based structure.

### Profile Management

**1. Add a new profile:**

```bash
ssh-commander add-profile
```

This will launch an interactive prompt to guide you through setting up a new profile.

**2. List available profiles:**

```bash
ssh-commander list
```

**3. Remove a profile:**

```bash
ssh-commander remove <profile_name>
```

### Executing Commands

**1. Run a single command:**

```bash
ssh-commander run <profile_name> "your_command_here"
```

Example:
```bash
ssh-commander run my-server "df -h"
```

**2. Run a macro:**

First, add a macro to your profile by editing `~/.ssh_commander.json`. Add a `"macros"` dictionary to your profile configuration:

```json
"my-server": {
  "host": "192.168.1.100",
  "user": "admin",
  ...
  "macros": {
    "status": [
      "uptime",
      "df -h",
      "free -m"
    ]
  }
}
```

Then, execute the macro:

```bash
ssh-commander macro <profile_name> <macro_name>
```

Example:
```bash
ssh-commander macro my-server status
```

### Interactive Shell

To start an interactive SSH session:

```bash
ssh-commander shell <profile_name>
```

You can then type commands as you would in a normal SSH session. Type `exit` or `quit` to end the session.

### Help

For a full list of commands and options:

```bash
ssh-commander --help
```

## Configuration File

- The configuration and profiles are stored in `~/.ssh_commander.json`.
- The first run will generate an encryption key for storing passwords securely.
- **Important**: It is recommended to back up this file. If the encryption key is lost, passwords will be unrecoverable.

## Session Logs

- All session output is logged to files in the `~/ssh_logs/` directory.
- Each log file is named with the profile and a timestamp, e.g., `my-server_20250630_123000.log`.
