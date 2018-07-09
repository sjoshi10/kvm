# kvm

This is a tutorial on how to's for create KVM guests. 

# Volume for Guest
`virsh vol-create-as <pool-name> <volume-name> 12G`

`virsh attach-disk <guest-name> --source /path/to/<volume-name> --target vdb --persistent`

`virsh detach-disk <guest-name> --source /path/to/<volume-name> --persistent`


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
