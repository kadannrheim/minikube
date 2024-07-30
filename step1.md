# Install and configurate OS
list of command:
reset: `sudo reboot now`
off: `poweroff -n`

1. LAN on ubuntu 24.04 netplan
    * see ours interfaces: `ls /sys/class/net`
    * edit config file `sudo vi /etc/netplan/02-networkd.yaml` 02- are other
        * static:
            ```
            network:
        renderer: networkd
        ethernets:
            enp0s8:
                dhcp4: no
                addresses: [ 192.168.0.110/24 ]
                routes: 
                  - to: default
                    via: 192.168.0.1 
                nameservers:
                addresses: [ 8.8.8.8, 8.8.4.4 ]
        version: 2
        p.s. In ubuntu 24 use `route` not `gateway4`
            ```
        * local:
            ```
            enp0s3:
                dhcp4: no
                addresses: [ 10.0.0.110/24 ]
            ```
    * Apply `sudo netplan generate` are for debug `sudo netplan --debug apply`
    * Definitely: `sudo netplan apply`
2. Enable in to password
    * Editing config, path: /etc/ssh/sshd_config
        `PasswordAuthentication yes`
    * Restart ssh `udo systemctl restart ssh`
    * Conect as ssh
3. Generating and use sertificat to connecting on ssh
* Generate key `ssh-keygen -t rsa`
* Save file `/home/kadannr/.ssh/id_rsa_main`
* Bothe machine had connect to ssh, used this command with st1:
    `cat ~/.ssh/id_rsa_main.pub | ssh kheim@kheim "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"`
    are with user machine: `ssh-copy-id kadannr@st1`

4. Use domain name to connecting on hostname. 
* This need fot ssh connecting. Added to ssh config `.ssh/config`:
    ```
Host t430
Hostname 192.168.0.15
User kheim

Host st1
Hostname 192.168.0.110
User kadannr
    ```
* This need for ping to hostname
Added in config `/etc/hosts` address and name:
```
192.168.0.15 t430
192.168.0.110 st1
```
p.s. /etc/hostname keeps name local machine and dont need edit fot this
5. Installing Ansible. Use official documentation https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu
```
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```
Cheking version: `ansible --version`
6. Installing vagrant. Use official documentationhttps://vegastack.com/tutorials/how-to-install-vagrant-on-ubuntu-22-04/
* 
```
sudo apt install virtualbox
vboxmanage --version
```
