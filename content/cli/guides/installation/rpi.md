---
title: "Install on Raspberry Pi OS"
weight: 5
menu:
  cli:
    parent: "cli_overview"
    identifier: "cli_installation_rpi"
    title: "Install on Raspberry Pi OS"
---

The TelemetryJet CLI uses [apt](https://en.wikipedia.org/wiki/APT_(software)) to manage installations on Linux-based environments. The CLI is distributed using our own third-party repository. These instructions are for Raspberry Pi OS and other ARM-based Linux environments.

### Import GPG Key
Releases on our repository are signed to verify authenticity. Run the following command to add the GPG key for the TelemetryJet releases:
<pre>
curl -fsSL https://downloads.telemetryjet.com/builds/cli/linux/armhf/repo/KEY.gpg | sudo apt-key add -
</pre>

### Add APT Repository
Add the TelemetryJet repository, which will allow apt to install TelemetryJet software from our download server:
<pre>
sudo sh -c "echo 'deb https://downloads.telemetryjet.com/builds/cli/linux/armhf/repo/ /' > /etc/apt/sources.list.d/telemetryjet.list"
sudo apt update
</pre>

### Installing
To install the CLI, run:
<pre>
sudo apt install telemetryjet-cli
</pre>

### Upgrading
To upgrade to the latest version, use apt's `update` and `upgrade` commands:
<pre>
# Pull the list of outdated software and update the CLI
sudo apt update
sudo apt upgrade telemetryjet-cli
</pre>

### Uninstalling
To uninstall the CLI, run:
<pre>
sudo apt remove telemetryjet-cli
</pre>

<br />

## Manual Installation
The TelemetryJet CLI can also be manually installed on Raspberry Pi OS. See [Manual Installation](/cli/guides/installation/manual_install/) for detailed instructions on how to manually install the CLI.