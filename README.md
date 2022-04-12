# Cheat sheet of multiple purposes
This document contains useful commands for everyday coding.
- [**git**](#git)
- [**file transfer**](#file-transfer)
- [**inspect files**](#inspect-files)
- [**compress files**](#compress-files)
- [**ssh related**](#ssh-related)
## git
### branching
delete branch: <br>
```
git branch -d <branch-name>
```
delete branch(force): <br>
```
git branch -D <branch-name>
```
delete remote branch: <br>
```
git push --delete <remote name> <branch name>
```
## file transfer
### scp
remote -> local (folder): <br>
```
scp -r user@address:~/remote_dir/ local_dir/
```
Note that this command will place the folder under `local_dir/` <br>
for a single file: <br>
```
scp user@address:~/remote_dir/file local_dir/
```
local -> remote:
```
scp local_dir/file user@address:~/remote_dir/ 
```

Other common used tags:

- `-P` - Specifies the remote host ssh port.
- `-p` - Preserves files modification and access times.
- `-q` - Use this option if you want to suppress the progress meter and non-error messages.
- `-C` - This option forces scp to compresses the data as it is sent to the destination machine.

### rsync(better than `scp` for large files)
Syntax almost identical to `scp`

remote -> local: <br>
```
rsync -avzh user@address:~/remote_dir/ local_dir/
```

local -> remote:
```
rsync -avzh local_dir/file user@address:~/remote_dir/
```
## inspect files
### ls
check size of specific file:
```
ls -l <FILENAME>
```
check sizes of all files in the current directory:
```
ls -l *
```
check sizes of all files including hidden files in the current directory:
```
ls -al * 
```
check size of all the files including hidden files in the ‘dir’ directory:
```
ls -al <DIR/>
```
### du
check disk usage of specific file:
```
du -s <FILENAME>
```
check disk usage summary of a directory tree and each of its subdirectories:
```
du <DIR/>
```
Common used tags(for both `ls` and `du`):

- `-h` - Makes file size more readable
## compress files
### tar
```
tar -czvf zipped_filename.tar.gz folder/
```

## ssh related
### ssh tunnel
```
ssh -L 8080:localhost:<PORT> <REMOTE_USER>@<REMOTE_HOST>
```
