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
                gateway4: 192.168.0.1
                nameservers:
                addresses: [ 8.8.8.8, 8.8.4.4 ]
        version: 2
            ```
        * local:
            ```
            enp0s3:
                dhcp4: no
                addresses: [ 10.0.0.110/24 ]
            ```
    * Apply `sudo netplan generate` are for debug `sudo netplan --debug apply`
2. Enable in to password
    * Editing config, path: /etc/ssh/sshd_config
        `PasswordAuthentication yes`
    * Restart ssh `udo systemctl restart ssh`
    * Conect as ssh