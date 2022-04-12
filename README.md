# Cheat sheet of multiple purposes
This document contains useful commands for everyday coding.
- **Git**
- **File transfer**
- **Compress files**
- **ssh related**
## Git
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
## File transfer
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

## Compress files
### tar
```
tar -czvf zipped_filename.tar.gz folder/
```

## ssh related
### ssh tunnel
```
ssh -L 8080:localhost:<PORT> <REMOTE_USER>@<REMOTE_HOST>
```
