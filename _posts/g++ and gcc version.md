# g++ and gcc version in Ubuntu
## check version
```bash
gcc --version
g++ --version
```
## Install version
```bash
sudo apt-get install -y gcc-4.7
sudo apt-get install -y g++-4.7
```
## Update version 
```bash
cd /usr/bin
sudo rm gcc
sudo ln -s gcc-4.7 gcc
sudo rm g++
sudo ln -s g++-4.7 g++
```
## check version
```bash
ls –al gcc g++
gcc --version
g++ --version
```
