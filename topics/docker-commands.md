# Docker Commands

```sh
# Install Docker on Ubuntu 18.04
sudo snap install docker

# Start Docker
sudo snap start docker

# Test Docker installation
sudo docker run hello-world

# Docker machine must be running before `docker-compose up` works
# List docker machines
docker-machine ls

# Create docker machine
docker-machine create --driver virtualbox <machine-name>
# e.g. docker-machine create --driver virtualbox default

# Remove docker machine
docker-machine rm <machine-name>

```