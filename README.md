# K8s on Raspberry Pi Cluster

## Setup

### Required Hard- and Software
* 2-N Raspberry Pi 4 B (4GB) incl. Power supply and Micro SD
* Install https://www.terraform.io/

### Install Ubuntu
1. Raspberry Pi Imager
2. Download latest LTS Version from https://ubuntu.com/download/raspberry-pi
3. Write Image to SD Card
4. Setup Wifi, see https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi#3-wifi-or-ethernet
5. Boot server

### Boot and first steps
1. Connect via SSH to ubuntu@<ip>
   password is: ubuntu
   and update the password
2. Generate RSA 4096 bit keypair
   ```
   ssh-keygen -o -t rsa -b 4096 -C "your@email-address.com"
   ```
3. Copy public key to Servers
   ```
   ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@<ip>
   ``` 
4. Update hostname within local network
   Show static hostname ``` hostnamectl ``` 
   Change static hostname ``` hostnamectl set-hostname k8s-cluster-master01 ``` ``` k8s-cluster-node01 ```
5. Reboot each server
   ```
   sudo reboot
   ```

### Connect to Server

Prepare ssh config file

```
Host master01
  HostName k8s-cluster-master01
  User ubuntu
  IdentityFile ~/.ssh/sshkeys/id_rsa_k8s_cluster

Host node01
  HostName k8s-cluster-node01
  User ubuntu
  IdentityFile ~/.ssh/sshkeys/id_rsa_k8s_cluster

```

## Terraform


