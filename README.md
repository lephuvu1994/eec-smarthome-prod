# Cập nhật hệ điều hành 
sudo apt update

sudo apt upgrade -y


# Cài đặt docker
curl -fsSL https://get.docker.com -o get-docker.sh

sudo sh get-docker.sh

sudo apt install -y docker-ce docker-ce-cli containerd.io

## Kiểm tra cài dặt docker 
docker --version

## Chạy docker không cần sudo
sudo usermod -aG docker $USER

newgrp docker


# Cài đặt docker compose

sudo curl -L "https://github.com/docker/compose/releases/download/v2.27.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

## Kiểm tra cài đặt docker compose
docker compose --version

# Create a directory for eecsmarthome and set your user as owner of it

sudo mkdir /opt/eecsmarthome

sudo chown -R ${USER}: /opt/eecsmarthome

# Clone Zigbee2MQTT repository
git clone --depth 1 https://github.com/lephuvu1994/eec-smarthome-prod.git /opt/eecsmarthome


# Install dependencies (as user "pi")
cd /opt/eecsmarthome

# Build docker image
docker build -t lephuvu/eecsmarthome-v3:1.0.14 .

# Run docker image
docker compose up -d
