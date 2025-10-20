# portainer-quick

A lightweight desktop GUI application for quickly managing Docker stacks through the Portainer API.

## Description

Portainer Quick is a Python-based desktop application that provides a simple and intuitive interface for managing your Docker stacks across one or more Portainer instances. Instead of navigating through the web interface, you can start and stop your Docker stacks directly from your desktop with just a click.

## Features

- **Quick Stack Management**: Start and stop Docker stacks with a single button click
- **Multi-Instance Support**: Manage stacks across multiple Portainer instances simultaneously
- **Real-time Updates**: Automatic refresh every 5 seconds to keep stack status current
- **Instance Filtering**: Filter displayed stacks by Portainer instance using a dropdown menu
- **Visual Status Indicators**: 
  - Green buttons for stopped stacks (click to start)
  - Red buttons for running stacks (click to stop)
- **Desktop Integration**: Launcher icon for easy access from your application menu
- **Status Notifications**: Popup messages confirm when stacks are started or stopped

## How It Works

The application connects to the Portainer API using your configured API key(s) and retrieves a list of all Docker stacks. Each stack is displayed with its name, associated Portainer instance, and current status. The interface provides immediate visual feedback and allows you to control stack states without leaving your desktop environment.

## Requirements

- Python 3
- pip 3

## Python Dependencies

The following Python dependencies will be installed during setup:

- **PyQt6**: GUI framework for the desktop interface
- **requests**: HTTP library for Portainer API communication

## Installation

```bash
git clone https://github.com/shimunmatic/portainer-quick.git
cd portainer-quick
chmod +x install.sh
./install.sh YOUR_API_KEY
```

The installation script will:
1. Copy application files to `~/.local/share/portainer-quick/`
2. Create an executable launcher in `~/.local/bin/`
3. Install a desktop entry for your application menu
4. Create a default configuration file at `~/.config/portainer-quick/config.json`
5. Install required Python dependencies (PyQt6)

## Usage

After installation, you can run the app using your application launcher or in terminal with:

```bash
portainer-quick
```

### First Run

On the first run, if no configuration file exists, a default configuration template will be created at `~/.config/portainer-quick/config.json`. You'll need to edit this file with the proper multi-instance format and add your Portainer instance details.

### Configuration

Edit `~/.config/portainer-quick/config.json` to configure your Portainer instance(s):

```json
{
  "instances": [
    {
      "name": "Production",
      "url": "https://portainer.example.com",
      "apiKey": "your-api-key-here"
    },
    {
      "name": "Development",
      "url": "http://localhost:9000",
      "apiKey": "your-dev-api-key"
    }
  ]
}
```

**Configuration Fields:**
- `name`: A friendly name for the Portainer instance (displayed in the UI)
- `url`: The full URL to your Portainer instance
- `apiKey`: Your Portainer API access token

**Obtaining an API Key:**
1. Log in to your Portainer web interface
2. Navigate to "My account" or "User settings"
3. Find the "Access tokens" section
4. Create a new access token
5. Copy the token to your configuration file

## Interface Overview

- **Instance Dropdown**: Select "All" to view stacks from all instances, or choose a specific instance
- **Sync Button**: Manually refresh the stack list
- **Stack List**: Scrollable list of all stacks with their current status
- **Stack Controls**: Each stack has a START (green) or STOP (red) button depending on its current state

## Technical Details

- Built with PyQt6 for cross-platform desktop GUI support
- Uses Portainer's REST API for stack management
- Configuration stored in JSON format
- Auto-refresh timer updates stack status every 5 seconds
- SSL certificate verification disabled for flexibility (use with trusted networks)
