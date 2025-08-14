# Ansible Role For Forensic Workstation Setup (Windows)

An Ansible role to install and configure essential forensic tools on Windows workstations, including Autopsy, Wireshark, VSCode (with extensions), FTK Imager, Volatility3, Procmon, PEStudio, and BrowserHistoryView.

## Requirements

- Windows hosts with WinRM enabled and configured for Ansible
- Python installed on the control machine
- Chocolatey should be allowed to install packages
- Administrative privileges on target machines

## Role Variables

All variables are optional unless noted otherwise:

| Variable | Default | Description |
|----------|---------|-------------|
| `tools_desktop_folder` | `"C:\\Users\\Public\\Desktop\\Forensic Tools"` | Folder to store all forensic tool shortcuts |
| `install_autopsy_version` | `"4.22.1"` | Version of Autopsy to install |
| `install_vscode_version` | `"1.103.0"` | Version of VSCode to install |
| `vscode_extensions` | `["redhat.ansible", "ms-python.python", "ms-vscode.powershell", "github.copilot"]` | List of VSCode extensions to install |

## Dependencies

No other roles are required. However, Chocolatey must be accessible for installing packages.

## Example Playbook

```yaml
- hosts: windows
  roles:
    - role: forensic_workstation_setup_windows
      vars:
        tools_desktop_folder: "C:\\Users\\Public\\Desktop\\Forensic Tools"
        install_autopsy_version: "4.22.1"
        install_vscode_version: "1.103.0"

