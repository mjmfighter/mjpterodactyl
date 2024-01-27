# Pterodactyl Wings setup

This guide is how to install wings on a server

## Prerequisites

Before you begin, make sure you have the following software installed:

- Docker and Docker Compose installed on your system. For instructions on how to install Docker on Linux, please refer to the official Docker documentation: [Install Docker on Linux](https://docs.docker.com/engine/install/
- Certbot for SSL certificates.  For Ubuntu 20/22, you can following these instructions: [Install Certbot Ubuntu](https://certbot.eff.org/instructions?ws=other&os=ubuntufocal)

## Installation

### Install wings

Use the following to install the wings binary

```bash
sudo mkdir -p /etc/pterodactyl
curl -L -o /usr/local/bin/wings "https://github.com/pterodactyl/wings/releases/latest/download/wings_linux_$([[ "$(uname -m)" == "x86_64" ]] && echo "amd64" || echo "arm64")"
sudo chmod u+x /usr/local/bin/wings
```

Next we want to setup the wings systemd service, so that wings will automatically start on system boot.  Create a file called `wings.service` in the `/etc/systemd/system` folder with the following contents:

```
[Unit]
Description=Pterodactyl Wings Daemon
After=docker.service
Requires=docker.service
PartOf=docker.service

[Service]
User=root
WorkingDirectory=/etc/pterodactyl
LimitNOFILE=4096
PIDFile=/var/run/wings/daemon.pid
ExecStart=/usr/local/bin/wings
Restart=on-failure
StartLimitInterval=180
StartLimitBurst=30
RestartSec=5s

[Install]
WantedBy=multi-user.target
```

### Configure wings

Now that we have wings installed, we need to grab the configuration so it knows where to connect to the panel.  To get this configuration, you will need to create a new node in the Nodes section in the panel.  After you have created the node in the panel, go into the Configuration tab and copy the Configuration File code block.  Create a file on the node called `config.yml` in the `/etc/pterodactyl` folder, paste that config in there, and save it.

### SSL Configuration

Before we can start the wings service, we need to ensure that it has SSL certificates or else it won't start properly.  To create the SSL certificates, you can use the following command.  Replace <fqdn> with your actual FQDN of the node.

```bash
certbot certonly --standalone -d <fqdn> --deploy-hook "systemctl restart wings"
```

### Enable wings service and start it

Now just enable and start wings

```bash
systemctl enable --now wings
```

After it starts up, it should appear as online in the panel.

## Support

For any assistance or queries, please refer to the documentation or open an issue in the repository.