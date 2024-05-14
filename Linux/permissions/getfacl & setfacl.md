**getfacl**:

- `getfacl` is a command-line utility used in Unix-like operating systems to view the access control lists (ACLs) of files and directories.
- ACLs provide a more granular level of permission management compared to traditional Unix permissions.
- It displays the ACL entries for the specified file or directory, including the users and groups with permissions, as well as any default ACLs.
- Syntax: `getfacl [options] [file/directory]`

**setfacl**:

- `setfacl` is a command-line utility used in Unix-like operating systems to set or modify the access control lists (ACLs) of files and directories.
- It allows users to define custom ACLs to grant or revoke specific permissions for users and groups.
- `setfacl` can be used to set both standard and default ACLs.
- Syntax: `setfacl [options] [file/directory]`

### Cheat Sheet:

|Command|Description|
|---|---|
|`getfacl file/directory`|View ACLs for a specific file or directory|
|`getfacl -R directory`|Recursively display ACLs for all files and subdirectories|
|`setfacl -m u:user:permissions file/directory`|Set permissions for a specific user|
|`setfacl -m g:group:permissions file/directory`|Set permissions for a specific group|
|`setfacl -x u:user file/directory`|Remove ACL entry for a specific user|
|`setfacl -x g:group file/directory`|Remove ACL entry for a specific group|
|`setfacl -b file/directory`|Remove all ACL entries for a file or directory|
|`setfacl -d -m u:user:default_permissions directory`|Set default permissions for a directory|
|`setfacl -k file/directory`|Remove default ACL entries for a file or directory|

This cheat sheet should help you quickly reference the basic usage of `getfacl` and `setfacl` commands.