In a container using miniconda, installation was successful using these commands:

```
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```
Say yes to appending miniconda path...
```
source .bashrc
conda install -c conda-forge pyne
```
Required ubuntu 16.04 packages:
```
wget
gcc
lsb-release
bzip-2
```
