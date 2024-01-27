# Repository Name

This repository contains the code for the Pterodactyl Panel.  It contains a modified version of the docker-compose file from the pterodactyl github repository.  This one adds support for automatically creating and renewing LetsEncrypt SSL certificates

## Prerequisites

- Docker installed: Please make sure Docker is installed on your system before proceeding. For instructions on how to install Docker on Linux, please refer to the official Docker documentation: [Install Docker on Linux](https://docs.docker.com/engine/install/#server)

## Getting Started

To start the Pterodactyl Panel, follow these steps:

1. Clone this repository to your local machine.
2. Install the necessary dependencies.
3. Run `docker compose pull` to pull the latest versions of the docker containers
4. Run `docker compose up -d` to start all the services
