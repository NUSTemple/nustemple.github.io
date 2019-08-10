# Install Cluster in 3 ubuntu mini pcs - part 2 (Host preparation)

## Installl Java (Optional as Ambari can install Java itself)
```bash
# Install Java
sudo apt install openjdk-8-jdk -y
# Check installation
java -version
```

## Create new group and user (Optional as root acount can be used)

```bash
# Create group
sudo addgroup hadoop
# Create user and password: ff
sudo adduser --ingroup hadoop hduser
sudo usermod -aG sudo hduser
```

## Prepare ssh (in case root account is used, update below settings for root)
```bash
# use hduser account and enter password
su hduser

# remove password for sudo access
sudo visudo
```
add below line at bottom of the file then save
> `hduser ALL=(ALL) NOPASSWD:ALL`

```bash
# generate ssh-keygen
ssh-keygen -b 4096

# Copy key to remote servers
ssh-copy-id -i $HOME/.ssh/id_rsa hduser@slave01
ssh-copy-id -i $HOME/.ssh/id_rsa hduser@slave02

# This will generate file authorized_keys under /home/hduser/.ssh/

# Check whether ssh is installed successfully
ssh hduser@slave01
ssh hduser@slave02
```

## Enable NTP on the Cluster and on the Browser Host
```bash
sudo apt-get install ntp -y
sudo update-rc.d ntp defaults
```

## Configuring iptables
```bash
sudo ufw disable
sudo iptables -X
sudo iptables -t nat -F
sudo iptables -t nat -X
sudo iptables -t mangle -F
sudo iptables -t mangle -X
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
```



