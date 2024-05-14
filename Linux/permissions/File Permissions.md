
| Permission   | Symbol | Explanation                                                                             | What You Can Do                                                                                    |
| ------------ | ------ | --------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| Read         | r      | Allows reading/viewing the contents of the file.                                        | View the contents of the file.                                                                     |
| Write        | w      | Allows modifying the contents of the file.                                              | Modify, edit, or delete the file.                                                                  |
| Execute      | x      | Allows executing the file if it's a program or script.                                  | Run the file if it's an executable program or script.                                              |
| Set User ID  | SUID   | Gives temporary permissions to a user running the file.                                 | Execute the file with the permissions of the file's owner, not the user executing it.              |
| Set Group ID | SGID   | Gives temporary permissions to a group running the file.                                | Execute the file with the permissions of the file's group, not the group of the user executing it. |
| Sticky Bit   | t      | Restricts the deletion of a file to its owner, the directory's owner, or the root user. | Prevents deletion of files by users other than the file owner, directory owner, or root.           |

### Cheat Sheet:

#### Using `chmod`:

|Command|Explanation|
|---|---|
|`chmod [who] [operator] [permissions] [file/directory]`|Change permissions using symbolic notation.|
|`chmod [mode] [file/directory]`|Change permissions using octal notation.|

#### Special Modes:

|Command|Explanation|
|---|---|
|`chmod u+s [file/directory]`|Set the SUID bit, giving temporary permissions to the user.|
|`chmod g+s [file/directory]`|Set the SGID bit, giving temporary permissions to the group.|
|`chmod +t [directory]`|Set the sticky bit, restricting file deletion.|

### Examples:

- Granting temporary root permissions to a script:

```bash
chmod u+s script.sh
```

- Ensuring new files in a directory are only deletable by their owners:

```bash
chmod +t directory
```
