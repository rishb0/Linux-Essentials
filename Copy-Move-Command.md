Essential commands for managing files and directories in Linux, including copying (`cp`) and moving/renaming (`mv`).

---

# `cp`

The `cp` command is used to copy files and directories in Linux.

### Syntax

```
cp [OPTION]... SOURCE DESTINATION
```

### Examples

1. Copy a file from one location to another:
   ```
   cp file.txt /home/user/Documents/
   ```

2. Copy a directory and its contents recursively:
   ```
   cp -r my_folder /home/user/backup/
   ```

3. Copy a file and preserve attributes (timestamps, ownership, etc.):
   ```
   cp -p file.txt /home/user/backup/
   ```

4. Copy multiple files to a directory:
   ```
   cp file1.txt file2.txt /home/user/backup/
   ```

5. Copy a file with verbose output:
   ```
   cp -v file.txt /home/user/Documents/
   ```

6. Copy a file but prompt before overwriting:
   ```
   cp -i file.txt /home/user/Documents/
   ```

7. Copy only newer files (to avoid overwriting newer versions):
   ```
   cp -u file.txt /home/user/backup/
   ```

8. Copy a symbolic link instead of its target:
   ```
   cp -P symlink /home/user/backup/
   ```

9. Copy a file to multiple destinations:
   ```
   cp file.txt /home/user/Documents/ /home/user/backup/
   ```




# `mv`

The `mv` command is used to move or rename files and directories in Linux.

## Syntax

```
mv [OPTION]... SOURCE DESTINATION
```

## Examples

1. Move a file to another directory:
   ```
   mv file.txt /home/user/Documents/
   ```

2. Rename a file:
   ```
   mv oldname.txt newname.txt
   ```

3. Move a directory:
   ```
   mv my_folder /home/user/backup/
   ```

4. Move multiple files to a directory:
   ```
   mv file1.txt file2.txt /home/user/Documents/
   ```

5. Rename a directory:
   ```
   mv old_folder new_folder
   ```

6. Move a file but prompt before overwriting:
   ```
   mv -i file.txt /home/user/Documents/
   ```

7. Move a file and provide verbose output:
   ```
   mv -v file.txt /home/user/Documents/
   ```

8. Force move a file without prompting:
   ```
   mv -f file.txt /home/user/Documents/
   ```

9. Backup an existing destination file before moving:
   ```
   mv --backup file.txt /home/user/Documents/
   ```

10. Move a file but prevent overwriting if the file exists:
   ```
   mv -n file.txt /home/user/Documents/
   ```

