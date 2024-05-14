
`fdisk` is a command-line utility used for disk partitioning in Linux. It allows users to create, delete, modify, and display partitions on a hard disk. `fdisk` operates directly on the disk's partition table, so caution is advised when using it to avoid data loss. Here are some key points:

- **Partition Creation**: Use `fdisk` to create new partitions on a disk. Specify the partition size, type, and starting/ending sectors.
    
- **Partition Deletion**: `fdisk` can delete existing partitions from a disk. This action permanently removes the partition and its data, so use with caution.
    
- **Partition Type**: Define the type of partition, such as Linux filesystem (83), Linux swap (82), or EFI system (ef).
    
- **Partition Table Display**: View the current partition table of a disk to see existing partitions and their details.
    
- **Write Changes**: After making changes to the partition table, use the `w` command to write the changes to disk. This operation is irreversible.
    

**Cheatsheet:**

|Command|Description|
|---|---|
|`fdisk -l`|List partitions on all disks|
|`fdisk /dev/sdX`|Start fdisk on disk /dev/sdX|
|`n`|Create a new partition|
|`d`|Delete a partition|
|`p`|Print the partition table|
|`t`|Change a partition's system id|
|`w`|Write table to disk and exit|
|`q`|Quit without saving changes|
