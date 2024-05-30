
curl -sSL https://get.docker.com | sh
sudo groupadd docker
sudo usermod -aG docker $USER

sudo apt update && apt upgrade -y
sudo apt install fail2ban ntpdate docker-compose-plugin

nano $HOME/.bashrc
--> export PIHOSTNAME=$HOSTNAME
source $HOME/.bashrc

docker build -t mirkowust/wateringpi:latest .
docker compose up -d
docker logs -f wateringpi


git clone https://github.com/drevil75/wateringpi.git

# laser tof


sudo apt-get install python-smbus i2c-tools
sudo raspi-config -> i2c einschalten, neustart
i2cdetect -y 1

# create a ramdisk for cache files
sudo mkdir /mnt/ramdisk
sudo nano /etc/fstab

# ramdisk
tmpfs /mnt/ramdisk tmpfs nodev,nosuid,size=128M 0 0
# deactivate logging of last file access
/dev/mmcblk0p2 / ext4 defaults,nodiratime,noatime 0 1
# forward logfiles to ramdisk
none /var/log tmpfs size=5M,noatime 0

sudo mount -a

# deactivate swapping
sudo dphys-swapfile swapoff %% sudo systemctl disable dphys-swapfile && sudo apt-get purge dphys-swapfile
# ------------
````