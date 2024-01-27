
# Docker Compose Configuration

This repository contains a Docker Compose configuration for setting up a multi-service environment with `nginx-proxy`, `acme-companion`, a `database` service, and a `panel` service.

## Prerequisites

Before you begin, make sure you have Docker and Docker Compose installed on your system. For instructions on how to install Docker on Linux, please refer to the official Docker documentation: [Install Docker on Linux](https://docs.docker.com/engine/install/

## Cloning the Repository

First, download or clone this repository to your local machine:

```bash
git clone https://github.com/mjmfighter/mjpterodactyl.git
cd mjpterodactyl
```

## Configuration

1. **Environment Variables:** 
   - Navigate to the `x-common` section in the `docker-compose.yml` file.
   - Update the environment variables under `database`, `panel`, and `mail` as per your requirements.

## Starting the Services

After configuring the environment variables, you can start the services using Docker Compose:

```bash
docker compose up -d
```

This command will start all the services defined in the `docker-compose.yml` file.

### Post first time startup

The inital startup of the panel service can take a few minutes, as it is creating all the database tables and default configuration settings.  To monitor the panel startup process, you can run the following command:

```bash
docker compose logs panel
```

After the panel is started and can be seen properly at your desired URL, you will need to create a user in the panel.  You can do so with the following command:

```bash
docker compose exec panel php artisan p:user:make
```

After the user has been created, you can visit the site and login.

## Stopping the Services

To stop the services, use the following command:

```bash
docker compose down
```

## Updating the Services

To update the services, use the following commands:

```bash
docker compose pull
docker compose down
docker compose up -d
```

## Additional Information

- Ensure that the network configurations and volume mappings in the `docker-compose.yml` file match your system's setup.
- For detailed information about each service configuration, refer to their respective documentation.

## Support

For any assistance or queries, please refer to the documentation or open an issue in the repository.
