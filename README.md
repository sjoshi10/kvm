# kvm

This is a tutorial on how to's for create KVM guests. 

# Create a volume and attach volume to Guest
`virsh vol-create-as <pool-name> <volume-name> 12G`

`virsh attach-disk <guest-name> --source /path/to/<volume-name> --target vdb --persistent`
