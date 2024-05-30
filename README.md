# wateringpi

## Setup Instructions
create raspi image  on SD
ssh water@wateringpi

cd $HOME

## Installation of Docker
curl -sSL https://get.docker.com | sh
sudo groupadd docker
sudo usermod -aG docker $USER

## Install & Update ubuntu 
sudo apt update && apt upgrade -y
sudo apt install git fail2ban ntpdate -y

## set Environment Varaible for docker container
nano $HOME/.bashrc
--> export PIHOSTNAME=$HOSTNAME
source $HOME/.bashrc


git clone https://github.com/drevil75/wateringpi.git

cd wateringpi
docker compose up -d

## Use Watering Pi
open your browser:

### swagger ui to configure the ports
http://wateringpi:8080/api/v3/ui/

### WebPage to UI for switch on/off the watering valves
http://wateringpi