# Cheat sheet of multiple purposes
This document contains useful commands for everyday coding.
- [**git**](#git)
- [**file transfer**](#file-transfer)
- [**inspect files**](#inspect-files)
- [**compress files**](#compress-files)
- [**ssh related**](#ssh-related)
- [**conda related**](#conda-related)
## git
### branching
delete branch: <br>
```
git branch -d <BRANCH_NAME>
```
delete branch(force): <br>
```
git branch -D <BRANCH_NAME>
```
delete remote branch: <br>
```
git push --delete <REMOTE_NAME> <BRANCH_NAME>
```
## file transfer
### scp
remote -> local (folder): <br>
```
scp -r user@address:~/<REMOTE_DIRNAME>/ <LOCAL_DIRNAME>/
```
Note that this command will place the folder at `user@address:~/<REMOTE_DIRNAME>/` under `<LOCAL_DIRNAME>/` <br>
for a single file: <br>
```
scp user@address:~<REMOTE_DIRNAME>/<FILENAME> <LOCAL_DIRNAME>/
```
local -> remote:
```
scp <LOCAL_DIRNAME>/<FILENAME> user@address:~/<REMOTE_DIRNAME>/
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
rsync -avzh user@address:~/<REMOTE_DIRNAME>/ <LOCAL_DIRNAME>/
```

local -> remote:
```
rsync -avzh <LOCAL_DIRNAME>/<FILENAME> user@address:~/<REMOTE_DIRNAME>/
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
ls -al <DIRNAME>/
```
### du
check disk usage of specific file:
```
du -s <FILENAME>
```
check disk usage summary of a directory tree and each of its subdirectories:
```
du <DIRNAME>/
```
Common used tags(for both `ls` and `du`):

- `-h` - Makes file size more readable
## compress files
### tar
```
tar -czvf zipped_filename.tar.gz <FOLDER_NAME>/
```

## ssh related
### ssh tunnel
```
ssh -L 8080:localhost:<PORT> <REMOTE_USER>@<REMOTE_HOST>
```

## conda related
### install conda for linux from terminal
```
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh
```
### conda environments
create environment:
```
conda create -n <ENV_NAME>
```
This creates empty environment and does not include python. <br/>

create environment with python:
```
conda create -n myenv python=<PYTHON_VERSION> <PACKAGE_NAME>
```
create environment with `environment.yml` config file:
```
conda env create -f environment.yml
```
activate environment:
```
conda activate <ENV_NAME>
```
create `environment.yml` file from current conda environment
```
conda env export --from-history | grep -v "prefix" > environment.yml
```
