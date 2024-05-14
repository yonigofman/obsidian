
- `umask` is a command-line utility used in Unix-like operating systems to control the default permissions for newly created files and directories.
- It works by subtracting the specified mask from the default permissions (usually 666 for files and 777 for directories) to determine the final permissions.
- The default permissions are usually set by the system administrator and can be modified by individual users to suit their needs.
- `umask` settings are expressed in octal notation, where each digit represents the permissions for the owner, group, and others respectively.
- Commonly used to enhance security by restricting default permissions.

### Cheat Sheet:

|Command|Description|
|---|---|
|`umask`|Display the current umask settings|
|`umask -S`|Display the current umask settings in symbolic format|
|`umask [octal]`|Set the umask to the specified octal value|
|`umask -p`|Display the current umask settings in octal format|
|`umask -S [symbolic]`|Set the umask using symbolic notation|

### Examples:

1. Display current umask settings:

```bash
umask
```

2. Display current umask settings in symbolic format:

```bash
umask -S
```

3. Set umask to restrict permissions for group and others:

```bash
umask 027
```

4. Display current umask settings in octal format:

```bash
umask -p
```

5.  Set umask using symbolic notation:
```bash
umask -S u=rwx,g=rx,o=rx
``` 

This cheat sheet should help you understand and utilize `umask` effectively for managing default permissions on your Unix-like system.