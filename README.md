# Cheat sheet of multiple purposes
This document contains useful commands for everyday coding.
- [**git**](#git)
- [**file transfer**](#file-transfer)
- [**inspect files**](#inspect-files)
- [**remove files**](#remove-files)
- [**compress files**](#compress-files)
- [**docker related**](#docker-related)
- [**ssh related**](#ssh-related)
- [**conda related**](#conda-related)
- [**jupyter notebook remote session**](#jupyter-notebook)
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

rsync through specific ssh port (default ssh port is 22)
```
rsync -avzh -e 'ssh -p <PORT_NUMBER>' --progress user@address:~/<REMOTE_DIRNAME>/ <LOCAL_DIRNAME>/
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

## remove files
delete all files with extension `.EXT` under certain directory recursively
```
find . -name '*.EXT' -type f -delete
```
run without `-delete` to inspect summary of files to be removed
```
find . -name '*.EXT'
```
## compress files
### tar
```
tar -czvf zipped_filename.tar.gz <FOLDER_NAME>/
```
## docker related
### build docker image 
from the same directory as the Dockerfile
```
docker build -t <IMAGE_NAME> .
```
### enable GPU usage in docker
Install `nvidia-container-toolkit` for Debian-based OS
```
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
sudo systemctl restart docker
```
Running docker image with GPU support
```
docker run --gpus all -it <IMAGE_NAME>
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
conda create -n <ENV_NAME> python=<PYTHON_VERSION> <PACKAGE_NAME>
```
create environment with `environment.yml` config file:
```
conda env create -f environment.yml
```
clone existing environment (do this in the base environment)
```
conda create --name <NEW_ENV_NAME> --clone <OLD_ENV_NAME>
```
activate environment:
```
conda activate <ENV_NAME>
```
create `environment.yml` file from current conda environment
```
conda env export | grep -v "^prefix: " > environment.yml
```
update existing conda environment with `environment.yml`
```
conda activate <ENV_NAME>
conda env update --file environment.yml --prune
```

## jupyter notebook
Connect to `notebook.ipynb` host on remote address. <br/>
remote terminal:
```
jupyter notebook --no-browser --port=8889 notebook.ipynb
```
local terminal:
```
ssh -N -L localhost:8888:localhost:8889 <REMOTE_USER>@<REMOTE_HOST>
```
Similar to [ssh tunnel](#ssh-tunnel)
