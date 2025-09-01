# Ansible Role For Forensic Workstation Setup (Windows)

An Ansible role to install and configure essential forensic tools on Windows workstations, including Autopsy, Wireshark, VSCode (with extensions), FTK Imager, Volatility3, Procmon, PEStudio, and BrowserHistoryView as well as all Eric Zimmerman tools (including KAPE).

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

No other roles are required. However, Chocolatey must be accessible for installing packages. KAPE (Kroll Artifact Parser and Extractor) must be downloadable from http://kape.zip.

## Tags

You can use tags to execute only specific parts of the role:

| Tag | Description |
|-----|-------------|
| `install-autopsy` | Installs Autopsy and creates its shortcut |
| `install-vscode` | Installs VSCode and its extensions |
| `install-wireshark` | Installs Wireshark and creates its shortcut |
| `install-volatility` | Installs Volatility3 and creates its shortcut |
| `install-zimmermantools` | Install all Eric Zimmerman tools and copies them to the designated folder (based on the artifcat they are analysing) |
| `install-ftk` | Install FTK Imager and creates its shortcut|
| `install-browserhistoryview` | Install BrowserHistoryView and creates its shortcut |
| `install-pestudio` | Install PeStudio and creates its shortcut | 
| `install-procmon` | Install ProcMon and creates its shortcut |
| `install-utilities` | Install some utilities (Libre Office, MobaXTerm, Notepad++, 7Zip) |
| `install-kape` | Install KAPE (Kroll Artifact Parser and Extractor) from `http://kape.zip` and verify the installation by running the included `Get-KAPEUpdate.ps1` script.|
| `verify-kape` | Run the `Get-KAPEUpdate.ps1` script to check and verify KAPE’s current version.|


To run only a specific section, use the `--tags` option with `ansible-playbook`. For example:

```bash
ansible-playbook -i hosts playbook.yml --tags install-autopsy
```
## Example Playbook

```yaml
- hosts: windows
  roles:
    - role: forensic_workstation_setup_windows
      vars:
        tools_desktop_folder: "C:\\Users\\Public\\Desktop\\Forensic Tools"
        install_autopsy_version: "4.22.1"
        install_vscode_version: "1.103.0"
```
**NB:** Please note that all shortcuts are available in `tools_desktop_folder` location.
