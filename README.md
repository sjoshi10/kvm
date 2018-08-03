# kvm

# Install KVM
https://www.linuxtechi.com/install-kvm-hypervisor-on-centos-7-and-rhel-7/

https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/virtualization_deployment_and_administration_guide/index

Kickstart Reference: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/installation_guide/sect-kickstart-syntax

This is a tutorial on how to's for create KVM guests. 

Add the following to ifcfg-em1:
```
NETWORKING=yes
HOSTNAME=maincentos
GATEWAY=192.168.1.1
BRIDGE=br0
```

Add the following to ifcfg-br0:
```
TYPE=Bridge
BOOTPROTO=dhcp
NAME=br0
DEVICE=br0
ONBOOT=yes
```

# Volume for Guest
`virsh vol-create-as <pool-name> <volume-name> 12G`

`virsh attach-disk <guest-name> --source /path/to/<volume-name> --target vdb --persistent`

`virsh detach-disk <guest-name> --source /path/to/<volume-name> --persistent`

# launch artifactory in Host
`docker run --name artifactory-pro -d -v /opt/jfrog/artifactory:/var/opt/jfrog/artifactory -p 8081:8081 docker.bintray.io/jfrog/artifactory-oss:latest`

# launch gitlab in host
`https://docs.gitlab.com/omnibus/settings/backups.html`


# Creating Logical Volumes

```
pvcreate sdb
vgcreate vmgroup /dev/sdb
vgs
lvcreate -L 275G -n vm_volume vmgroup
yum -y install gfs2-utils
mkfs.gfs2 -p lock_nolock -j 1 /dev/vmgroup/vm_volume 
mkdir /vm-volume
mount /dev/vmgroup/vm_volume /vm-volume
```

moving logical volume to different host - http://tldp.org/HOWTO/LVM-HOWTO/recipemovevgtonewsys.html

# Launch VM

```
virt-install --name kubetest --memory 4096 --vcpus 2 --disk /vm-data/rootvol  --location /tmp/CentOS-7-x86_64-Minimal-1804.iso --os-variant linux --initrd-inject ks.cfg --extra-args="ks=file:/ks.cfg console=tty0 console=ttyS0,115200n8" --nographics
```

# Install LDAP
```
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install 389-ds-base
yum install 389-ds
setup-ds-admin.pl
```
http://directory.fedoraproject.org/docs/389ds/download.html

`systemctl start dirsrv-admin`

# Using LDAP
https://access.redhat.com/documentation/en-US/Red_Hat_Directory_Server/8.2/html/Administration_Guide/Examples-of-common-ldapsearches.html

https://access.redhat.com/documentation/en-US/Red_Hat_Directory_Server/8.2/html/Administration_Guide/Configuring_Directory_Databases.html

`ldapsearch -D "cn=directory manager"  -p 389 -b "dc=npmake,dc=io" -s sub "(objectclass=*)" -h ldap.npmake.io -w password`

add user: `ldapmodify -D "cn=directory manager"  -p 389 -h ldap.npmake.io -w password -f saurab.ldif`
