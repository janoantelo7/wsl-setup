# wsl-setup
Automated installation for **Ubuntu on WSL2** using **Cloud-init** and **Ansible**.

# Prerequisites
- Windows 11 with WSL2 enabled.
- Ubuntu distribution for WSL.

# How it's works
- Create a folder inside your Windows home called `.cloud-init` and paste the `ubuntu-all.user-data` inside it.
- Install WSL and an Ubuntu distro.

# System Configuration
- The `ubuntu-all.user-data` file is on charge of the first configuration:
  - **Locale & Timezone:** Sets locale to `es_ES.UTF-8` and timezone to `Europe/Madrid`.
  - **User Management:** Creates a default user with passwordless `sudo` access.
  - **WSL Settings:** Configures `/etc/wsl.conf` to enable `systemd` and set the default user.
  - **Auto-provisioning:** Automatically pulls and runs the Ansible playbook upon initialization.
- The `ubuntu.yml` playbook installs and configures the following:
  - **Core Packages:** `git`, `curl`, `vim`, `htop`, `ripgrep`, `unzip`.
  - **Python Tooling:** Installs [uv](https://github.com/astral-sh/uv) (an extremely fast Python package installer and resolver).
  - **SSH Integration:** Installs and configures [wsl2-ssh-agent](https://github.com/mame/wsl2-ssh-agent) globally in `/usr/local/bin` for seamless SSH key usage between Windows and WSL.

## Personalization
1.  **Customize User:**
    * Update the `users` section in `cloud-init/ubuntu-all.user-data`.
    * Update the `user_name` variable in `ubuntu.yml`.

## SSH Agent Integration
The setup automatically installs `wsl2-ssh-agent` to bridge your Windows SSH keys to WSL.
* **Binary Location:** `/usr/local/bin/wsl2-ssh-agent`
* **Auto-start:** The initialization command is automatically added to the user's `.bashrc`.

*Note: Ensure the "OpenSSH Authentication Agent" service is running on Windows.*

# License
This project is licensed under the [MIT License](LICENSE).
