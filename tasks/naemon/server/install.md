# Naemon Server

1. Create Linux VM using [Kickstart](https://github.com/927technology/kickstart).  Use your preferred hypervisor.

    1. Rock Linux 9.Latest
    1. 2 Processors
    1. 2 GB Ram
    1. 36 GB Storage
    1. Bridged Network

1. Enable root ssh

    `echo PermitRootLogin yes >> /etc/ssh/sshd_config`
    
    `systemctl restart sshd`

1. SSH into VM

    `ssh root@<ip address>`

1. Install Naemon repisitory
  
    `yum install -y wget`

    `wget -O /etc/yum.repos.d/naemon.repo https://download.opensuse.org/repositories/home:/naemon/AlmaLinux_9/home:naemon.repo`

    `yum check-update`

1. Install Naemon

    `yum install -y naemon`

1. Open firewall ports

    `firewall-cmd --permanent --add-port=80/tcp`

    `firewall-cmd --permanent --add-port=443/tcp`

    `firewall-cmd --reload`

1.  Enable services
    `systemctl enable httpd`

    `systemctl enable naemon`
    
1.  Configure SELinux

    `setenforce 0`

    `sed -i 's/SELINUXTYPE=targeted/SELINUXTYPE=minimum/g' /etc/selinux/config`

1.  Start Services

    `systemctl start httpd`

    `systemctl start naemon`

1. Login

    `http://<ip address>/naemon`
    
    \- OR -

    `https://<ip address>/naemon`

1. Reboot and ensure everything starts
    