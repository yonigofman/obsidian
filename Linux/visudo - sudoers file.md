
Visudo is a command-line utility used to safely edit the sudoers file in Unix-like operating systems. The sudoers file controls who can run what commands as what users on specific machines and can also specify options like whether to require a password. Visudo provides a safe way to edit this file by checking for syntax errors before saving changes, thus preventing potential misconfigurations that could lock users out of their system. It opens the sudoers file in a text editor specified by the EDITOR environment variable.

**Cheatsheet Table:**

|Command|Description|
|---|---|
|`sudo visudo`|Opens the sudoers file for editing in the default text editor specified by the EDITOR environment variable.|
|`visudo -c`|Checks the sudoers file for syntax errors without saving changes.|
|`visudo -f [filename]`|Edits a specific sudoers file instead of the default (`/etc/sudoers`).|
|`visudo -s`|Edits the sudoers file in strict mode, preventing the use of shortcuts like '!' for negation.|
|`visudo -x`|Parses the sudoers file and dumps the parsed output in XML format.|
|`visudo -V`|Displays the version of visudo.|

**Tips:**

1. Always use `sudo visudo` to edit the sudoers file to ensure proper permissions.
2. Verify the changes with `visudo -c` before saving to prevent syntax errors.
3. Take care when editing the sudoers file as incorrect configurations can lock users out of system privileges.
4. Backup the sudoers file before making changes (`sudo cp /etc/sudoers /etc/sudoers_backup`).
5. Document any changes made to the sudoers file for reference and troubleshooting.

### Structure

```sudoers
user    hosts=commands     options
```

- **User**: Specifies the users or groups to whom the rule applies. Use `%groupname` to specify a group.
- **Hosts**: Defines the hosts or machines where the rule is effective. Use `ALL` for all hosts or specify specific hostnames.
- **Commands**: Lists the commands or command patterns users can run. Use `ALL` to allow any command or specify specific commands.
- **Options**: Additional settings such as NOPASSWD (no password required), NOTTY (can't run commands from a non-terminal session), etc.
#### Examples

```bash
# Allow user 'john' to run all commands as any user without password john 
ALL=(ALL:ALL) ALL
# Allow members of the 'admin' group to run any command as root without password
%admin ALL=(ALL:ALL) NOPASSWD:ALL
# Allow user 'mary' to run '/bin/ls' and '/bin/cat' as root without password
mary ALL=(ALL:ALL) NOPASSWD:/bin/ls, /bin/cat
# Allow user 'admin' to create users starting with 'appuser' without password
admin ALL=(ALL:ALL) NOPASSWD: /usr/sbin/useradd appuser*
# Allow user 'admin' to create users with specific parameters without password
admin ALL=(ALL:ALL) NOPASSWD: /usr/sbin/useradd -m -s /bin/bash appuser*
# Allow user 'webadmin' to restart the nginx service without password webadmin
ALL=(ALL:ALL) NOPASSWD: /bin/systemctl restart nginx
```



