# Set up local development environment

1. Install the following software:

- Windows Terminal
- VS Code
- Visual Studio Community (for desktop development)
- Bruno Client
- Navicat (or any other postgreSQL GUI)

2. Install the follow VSCode plugins


3. Install the following inside of Windows Terminal:

- Ubuntu
- PostgreSQL
- Redis
- Git
- [Github CLI (gh cli)](https://github.com/cli/cli/blob/trunk/docs/install_linux.md)
- Python3
- [NodeJS (nvm)](https://nodejs.org/en/download)

```bash
# Download and install nvm:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# in lieu of restarting the shell
\. "$HOME/.nvm/nvm.sh"

# Download and install Node.js:
nvm install 22

# Verify the Node.js version:
node -v # Should print "v22.18.0".
nvm current # Should print "v22.18.0".

# Verify npm version:
npm -v # Should print "10.9.3".
```
- [PM2](https://pm2.keymetrics.io/docs/usage/quick-start/)

```bash
npm install pm2@latest -g
```

- [serve](https://github.com/vercel/serve)

```bash
npm install -g serve
```

- [Docker](https://docs.docker.com/engine/install/ubuntu/)
- [Docker Compose Plugin](https://docs.docker.com/compose/install/linux/#install-using-the-repository)
- Set Docker to work without running "sudo"

```bash
# Create the docker group (if it doesn't exist)
sudo groupapp docker

# Add the user to the docker group
sudo usermod -aG docker $USER

# Apply the group changes by logging out and back in

# Now you can run the following command without "sudo"
docker ps 
```

- Docker Images (This is provided in docker-compose.yaml file)
  - Minio (S3 bucket)
  - MongoDB v8.0.12 (database)
  - Mongo Express UI (gui for database)

```yaml
services:
  mongodb:
    image: mongo:latest # version 8.0.12
    container_name: mongodb
    restart: unless-stopped
    hostname: mongodb
    ports:
      - "27017:27017"
    environment: # If want to add username + password access
      MONGO_INITDB_ROOT_USERNAME: mongoadmin
      MONGO_INITDB_ROOT_PASSWORD: mongopassword
    volumes:
      - mongo-data:/data/db
  minio:
    restart: unless-stopped
    container_name: minio
    image: "minio/minio:latest"
    ports:
      - "${FORWARD_MINIO_PORT:-9000}:9000"
      - "${FORWARD_MINIO_CONSOLE_PORT:-9090}:9090"
    environment:
      MINIO_ROOT_USER: "minioadmin"
      MINIO_ROOT_PASSWORD: "minioadmin"
      MINIO_ACCESS_KEY: "my-client-id"
      MINIO_SECRET_KEY: "my-secret-key"
    volumes:
      - "./minio-data:/data/minio"
    command: minio server /data/minio --console-address ":9090"

  mongo-express:
    depends_on:
      - mongodb
    image: mongo-express
    container_name: mongo-express
    restart: unless-stopped
    ports:
      - "8081:8081"
    environment: # If want to add username + password access
      ME_CONFIG_MONGODB_ADMINUSERNAME: mongoadmin
      ME_CONFIG_MONGODB_ADMINPASSWORD: mongopassword
      ME_CONFIG_MONGODB_SERVER: mongodb
      ME_CONFIG_BASICAUTH_USERNAME: mongouser
      ME_CONFIG_BASICAUTH_PASSWORD: password

volumes:
  mongo-data:
  minio-data:
```

4. Create databases and assign a password to postgresql
```
# Create database
CREATE DATABASE "mydatabase";

# Assign password
ALTER USER postgres PASSWORD 'postgres';

# Remove database
DROP DATABASE "mydatabase";
```

5. Set up Minio so that buckets are public (private by default)

```bash
# Have the minio docker container running, make sure you know the name

# Note the MINIO_ROOT_USER and MINIO_ROOT_PASSWORD in docker-compose.yaml file

# Execute a shell inside the docker container
docker exec -it minio sh

# Run mc from your container shell, log in as a user "myminio" with credentials
mc alias set myminio http://localhost:9000 <MINIO_ROOT_USER> <MINIO_ROOT_PASSWORD>

# Get list of buckets
mc ls myminio

# Get status of bucket
mc anonymous get myminio/bcapp-dev-assets

# Make the bucket public
mc anonymous set public myminio/bcapp-dev-assets
```