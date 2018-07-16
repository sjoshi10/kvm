# kvm

# Install KVM
https://www.linuxtechi.com/install-kvm-hypervisor-on-centos-7-and-rhel-7/

This is a tutorial on how to's for create KVM guests. 

Add the following to ifcfg-em1:
```
NETWORKING=yes
HOSTNAME=maincentos
GATEWAY=192.168.1.1
BRIDGE=br0
```
Add the following to ifcfg-br0:

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
