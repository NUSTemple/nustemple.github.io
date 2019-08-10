# Install Cluster in 3 ubuntu mini pcs - part 4 (Ambari UI Install)

## Start ambari-server
```bash
sudo ambari-server start
```

## Ambari UI
Incase ambari is installed on `master01` host, go to `http:\\master01:8080` to open the Ambari Install Wizard
The default username and password is both `admin` 

## Add host in UI
```bash
master01
slave01
slave02
```

## Add private key
Upload the private key which is used in part 1




## In case mysql driver is not available use below command to add mysql driver
```bash
wget http://repo.mysql.com/apt/ubuntu/pool/mysql-tools/m/mysql-connector-java/mysql-connector-java_8.0.17-1ubuntu18.04_all.deb

dpkg -i mysql-connector-java_8.0.17-1ubuntu18.04_all.deb
ls -al /usr/share/java/mysql-connector-java-8.0.17.jar

cd /var/lib/ambari-server/resources/
ln -s /usr/share/java/mysql-connector-java.jar mysql-connector-java.jar
```