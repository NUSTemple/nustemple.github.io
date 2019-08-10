# Install Cluster in 3 ubuntu mini pcs - part 1 (Hardware part)

## Preparation 
### Hardware

##### 3 INTEL NUC including charger
- 1 INTEL I7 + 32GB RAM + 512 SSD
- 2 INTEL I5 + 16GB RAM + 256 SSD
##### 1 Router
##### 4 WLAN cable
##### 1 power strip bar (At least 4 plug points)
##### 1 thumb drive with Ubuntu 18.04 LTS installed
##### 1 monitor and 1 set of wireless keyboard/mouse


## OS Installation

1. Install Ubuntu __18.04.2__ LTS version (tried on 18.04.03 version also but some error seen during the installation) in Intel NUC and label the NUC
    - I named 3 NUC as below
        - master01
        - slave01
        - slave02
2. Account:
    - username: pengtan
    - password: abc
3. Some options during the analysis:
    - no automatic update

4. After install system
    - update .bashrc 
    - install ssh ```sudo apt-get install ssh```
    - install cifs ```sudo apt-get install cifs-utils```
    - install smbclient ```sudo apt-get install smbclient samba```
5. mount thumb drive
    - for `master01`
    ```bash
    # Use `fdisk -l` to find device
    sudo fdisk -l
    
    sudo mkdir /nfs
    sudo mount /dev/sda1 /nfs -o umask=000
    ```
5. update smb conf
    Edit `/etc/samba/smb.conf` and Enable this `/nfs` folder in the samba by adding below lines at bottom
    ```bash
    [nfs]
      comment = my nfs folder
      path = /nfs
      read only = no
      guest ok = yes
    ```
    Restart the samba server
    ```bash
    sudo /etc/init.d/smbd restart
    ```
       
    - for `slave01` and `slave02`:
    Check whether samba folder is available
    
     ```bash
     smbclient -L //master01 --user=pengtan
     ```

    ```bash
    sudo mkdir /nfs
    sudo mount -t cifs -o user=pengtan -w //master01/nfs /nfs
    ```
    
6. Edit host file for each nuc
    ```bash
    sudo vi /etc/hosts
    ```
    add below lines (ip address might change based your own router config)
    > 192.168.1.169 master01
    > 192.168.1.21 slave01
    > 192.168.1.235 slave02
    
    can use `hostname -f` to check whether hostname is setup correct
    
    

