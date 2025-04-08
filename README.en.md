# Serveo Self-Hosted - Installer

Serveo is a tool that allows you to expose local ports from your Linux server via SSH, similar to ngrok but self-hosted.

## Requirements
- Linux system (amd64/x86_64 architecture only)
- Root permissions
- Internet connection (to download the installer)

## Installation

1. **Download the installer**:
   ```bash
   curl -O https://raw.githubusercontent.com/HirCoir/Self-Hosted-Serveo/refs/heads/main/install
   ```

2. **Make it executable**:
   ```bash
   chmod +x install
   ```

3. **Run the installer with sudo**:
   ```bash
   sudo bash install
   ```

### Installation options

You can customize the installation with these arguments:

- **Specify port** (default: 2222):
  ```bash
   sudo bash install -p 4444
   # or
   sudo bash install --port 4444
   ```

- **Specify public IP** (auto-detected by default):
  ```bash
   sudo bash install -h 192.168.1.100
   # or
   sudo bash install --host 192.168.1.100
   ```

- **Remove existing installation**:
  ```bash
   sudo bash install --remove
   ```

## Post-installation usage

Once installed, Serveo will run as a systemd service named `serveo`.

**Useful commands**:

- Check service status:
  ```bash
   sudo systemctl status serveo
   ```

- Start/stop/restart:
  ```bash
   sudo systemctl start serveo
   sudo systemctl stop serveo
   sudo systemctl restart serveo
   ```

- View logs:
  ```bash
   journalctl -u serveo -f
   ```

## Connecting from a client

To expose a local port (e.g., 3000) through your Serveo instance:
```bash
ssh -p <SERVEO_PORT> -R 8080:localhost:3000 <SERVER_IP>
```

## File locations
- Binary: `/opt/serveo/serveo`
- SSH keys: `/opt/serveo/ssh_host_rsa_key`
- Systemd service: `/etc/systemd/system/serveo.service`

## Credits
Developed by HirCoir  
Repository: https://github.com/HirCoir/self-hosted-serveo