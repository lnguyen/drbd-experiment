# DRBD Experiment

Experiment to play with drbd within vagrant

## Usage

Boot up machines and provision server
```
vagrant up
```

On both machines [drbd-0, drbd-1] as root, create volumes 

```
drbdadm create-md r0
drbdadm attach r0
```

On drbd-0, promote to primary. create filesystem and mount drive

```
drbdadm primary r0
mkfs.ext3 /dev/drbd1
mount /dev/drbd1 /mnt/drbd
```

Now that we have filesystem mount we can create files on new mount 
On drbd-0, create new files, unmount and demote to secondary
```
cd /mnt/drbd
touch my awesome new files
cd /mnt
umount /mnt/drbd
drbdadm secondary r0
```

On drbd-1, promote to primary, and mount drive
```
drbdadm primary r0
mount /dev/drbd1 /mnt/drbd
ls /mnt/drbd
```




