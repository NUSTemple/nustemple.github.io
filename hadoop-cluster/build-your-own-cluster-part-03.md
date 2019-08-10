# Install Cluster in 3 ubuntu mini pcs - part 3 (Installation)


## Install Ambari-server repo
```bash
sudo wget -O /etc/apt/sources.list.d/ambari.list http://public-repo-1.hortonworks.com/ambari/ubuntu18/2.x/updates/2.7.3.0/ambari.list

sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com B9733A7A07513CAD

sudo apt-get update
```

```bash
# check repo
sudo apt-cache showpkg ambari-server
```

## Install Ambari-server
```bash
sudo apt-get install ambari-server
```

## ambari-server setup
```bash
sudo ambari-server setup

# Press Enter all the way to complete the setup
```
