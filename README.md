# some-commands-for-ubuntu-20.04

## install cuda-toolkit in wsl-2 ubuntu
Source[https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=WSL-Ubuntu&target_version=2.0&target_type=deb_local]
```bash
wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/13.1.1/local_installers/cuda-repo-wsl-ubuntu-13-1-local_13.1.1-1_amd64.deb
sudo dpkg -i cuda-repo-wsl-ubuntu-13-1-local_13.1.1-1_amd64.deb
sudo cp /var/cuda-repo-wsl-ubuntu-13-1-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-toolkit-13-1
```
To add nvcc to path
Open: ```bash nano ~/.bashrc```
paste:
```bash
export PATH=/usr/local/cuda-13.1/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-13.1/lib64:$LD_LIBRARY_PATH
```
Save and Exit: Press Ctrl+O, then Enter, then Ctrl+X.
Reload the settings (Crucial):
```bash
source ~/.bashrc
```
> [!Note]
> You might have to update the windows nvidia drivers:
> Go to nvidia download page
> select your gpu, sytem config
> Download and install latest driver
> Shutdown wsl
Now try running cuda codes.

## How to increase swap memory:
Source[https://arcolinux.com/how-to-increase-the-size-of-your-swapfile/]  

Turn off all swap processes
```console
sudo swapoff -a
```
Resize the swap (from 512 MB to 8GB)  
```console
sudo dd if=/dev/zero of=/swapfile bs=1G count=8
```
if = input file  
of = output file  
bs = block size  
count = multiplier of blocks  

    
Make the file usable as swap

```console
sudo mkswap /swapfile
```
Activate the swap file

```console
sudo swapon /swapfile
```
Check the amount of swap available

```console
grep SwapTotal /proc/meminfo
```

## To add a path to linux environment variable:
### Add it to your ~/.profile or ~/.bashrc file. 

```console
export PATH="$PATH:/path/to/dir"
```

to create symlink to binaries:
```console
cd /usr/bin
sudo ln -s /path/to/binary binary-name
```

This will not automatically update your path for the remainder of the session. To do this, you run:

```console
source ~/.profile
```
or
```console
source ~/.bashrc
```

## How to make apple's macos image preview like feature in ubuntu
```console
sudo apt-get update
sudo apt-get install gnome-sushi
```

## To extract integers from a string

```console
import re
s = "checking skr (2, 3, 4, 6, -2, 12)"
#Find all integers (including negative numbers)
numbers = list(map(int, re.findall(r'-?\d+', s)))
```
re.findall(r'-?\d+', s):
\d+ matches one or more digits.
-? optionally matches a minus sign (for negative numbers).
map(int, ...) converts all matched strings to integers.
list(...) converts the map object to a list.
