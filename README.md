# ubuntu-system-reinstall
This is a manual that shows the detailed instructions to setup a development environment on Ubuntu 16.04 step by step.
## Setup Chinese Input Method
* Install Chinese for Ubuntu system
```
System Settings -> Language Support -> Update -> Install/Remove Languages -> Check Chinese
```
* Install ibus for input method
```
sudo apt-get install ibus ibus-clutter ibus-gtk ibus-gtk3 ibus-qt4
```
* Set ibus as system input method framework
```
im-config -s ibus
```
* Install ibus-pinyin and set it as main input method. (Reboot is required, otherwise we can not
  find the installed ibus-pinyin)
```
sudo apt-get install ibus-pinyin
sudo reboot
sudo ibus-setup
```
## Install ZSH
* Install git, curl and zsh. (Reboot is required.)
```
sudo apt-get install git
sudo apt-get install curl
sudo apt-get install zsh
zsh -version
sudo reboot
```
* Install oh-my-zsh. (Reboot is required)
```
sudo chsh -s $(which zsh)
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
sudo reboot
```
## Install Tmux
```
sudo apt-get install tmux
```
## Install & Setup Gvim
* Install gvim
```
sudo apt-get install vim-gtk
```
* Setup spf13-vim style
```
curl http://j.mp/spf13-vim3 -L -o - | sh
copy .vimrc .vimrc.local .vimrc.bundle .vimrc.before to Home directory
:PlugginInstall in Gvim
```
* Install YouCompleteMe
```
cd .vim/bundle/
git clone --recursive https://github.com/Valloric/YouCompleteMe.git
sudo./install.py –clang-completer
copy .ycm_extra_conf.py to .vim/bundle/YouCompleteMe/third_party/ycmd/cpp/ycm
```
## Install OpenCV 3.2.0
* Install dependencies
```
sudo apt-get install build-essential
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
```
* Install OpenCV-3.2.0
```
cd ~/opencv-3.2.0
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..
cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-3.4.1/modules .. (for opencv_contrib)
make -j7 # runs 7 jobs in parallel
sudo make install
```
## Install ros-kinetic
* Add reporsitory
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
sudo apt-get update
```
* Install ros-kinetic
```
sudo apt-get install ros-kinetic-desktop-full
```
* rosdep init and environment configuration
```
sudo rosdep init
rosdep update
echo "source /opt/ros/kinetic/setup.zsh" >> ~/.zshrc
source ~/.zshrc
```
## Install Eigen-3.3.4
```
cd Eiigen-3.3.4
mkdir build
cd build
cmake ..
sudo make install
```
## Install Ceres-1.13
* Installl Dependencies
```
sudo apt-get install cmake
sudo apt-get install libgoogle-glog-dev
sudo apt-get install libatlas-base-dev
sudo apt-get install libsuitesparse-dev
```
* Install Ceres-1.13
```
cd Ceres-1.13
mkdir build
cd buid
cmake ..
make -j3
make test
make install
```
## Install Pylon
```
cd pylon-5.0.11*
sudo tar -C /opt -xzf pylonSDK*.tar.gz
```
## Install cpprest
```
git clone --recursive https://github.com/Microsoft/cpprestsdk.git
cd cpprestsdk && cd Release
mkdir build
cmake ..
make -j4
sudo make install
```
## Install Zeal
```
sudo add-apt-repository ppa:zeal-developers/ppa
sudo apt-get update
sudo apt-get install zeal
```
## Install SSH
```
sudo apt-get install ssh
```
## Install Google-Chrome
```
sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -
sudo apt-get update
sudo apt-get install google-chrome-stable
```
## Install shadowsocks-qt5
```
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```
## Install Numpy
```
sudo apt-get install python-pip
pip install --upgrade pip
sudo pip install numpy
pip install numpy
```
## Install Matlab2018a
* Download the installation files from the official website or the Internet
* Mount the iso file one
```
cd /media
mkdir matlab
mount -o loop path/to/R2018a_glnxa64_dvd1.iso /media/matlab
```
* Installation
```
sudo ./matlab/install
choose standlone installation, input the key, and next.
mount -o loop path/to/R2018a_glnxa64_dvd2.iso /media/matlab
choose continue
```

## Install Texlive-2018
* Download the texlive2018 iso file
```
cd Downloads
wget http://mirrors.ctan.org/systems/texlive/Images/texlive2018.iso
```
* Mount iso file
```
sudo mkdir /media/cdimage
mount -o loop ~/Downloads/texlive2018.iso /media/cdimage
```
* Install texlive-2018
```
cd /media/cdimage
sudo perl install-tl
```
* Setup environment variables (for zsh shell)
```
sudo givm ~/.zshrc
export PATH=/usr/local/texlive/2018/bin/x86_64-linux:$PATH
export MANPATH=/usr/local/texlive/2018/texmf-dist/doc/man:$MANPATH
export INFOPATH=/usr/local/texlive/2018/texmf-dist/doc/info:$INFOPATH

```
## Install Cuda & Cudnn (Nvidia GTX1060)
### Install nvidia driver
* Install Dependencies
```
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler 
sudo apt-get install --no-install-recommends libboost-all-dev
sudo apt-get install libopenblas-dev liblapack-dev libatlas-base-dev
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
```
* Install nvidia driver
nvidia-384 is suitable for GTX 1060, and nvidia-391 is suitable for GTX 1080 and above
```
sudo add-apt-repository ppa:xorg-edgers/ppa
sudo apt-get update
sudo apt-get install nvidia-384
sudo reboot (to close the secure boot)
```
Then reboot, in the menu choose "change secure boot options", put the password you previously chose and disable the secure boot.

* Disable the integrated graphic driver(optional)
```
sudo chmod 666 /etc/modprobe.d/blacklist.conf
sudo gedit /etc/modprobe.d/blacklist.conf
```
add the following lines
```
blacklist vga16fb
blacklist nouveau
blacklist rivafb
blacklist rivatv
blacklist nvidiafb
```
close nouveau
```
echo options nouveau modeset=0 | sudo tee -a /etc/modprobe.d/nouveau-kms.conf
update-initramfs -u
sudo reboot
```
* Install kernel source
```
apt-get install linux-source  
apt-get install linux-headers-x.x.x-x-generic 
```
* Check whether the installation is successful
```
sudo nvidia-smi
```
### Install cuda
* Download the source file
Visit the website https://developer.nvidia.com/cuda-downloads and download the suitable version of cuda
* Install
```
sudo sh cuda_9.0.176_384.81_linux.run (cuda 9.0 is suitable for nvidia-384)
```
* Setup PATH and LD_LIBRARY__PATH
```
export PATH=/usr/local/cuda-9.0/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64:$LD_LIBRARY_PATH

```
* Verify the installation
```
/usr/local/cuda/samples/1_Utilities/deviceQuery
sudo make
sudo ./deviceQuery
```
### Install cudnn
* Download the source file
Visit the website https://developer.nvidia.com/rdp/cudnn-download, login, and download the suitable version of cudnn(7.1)

* Install
```
tar -xzf cudnn-9.0-linux-x64-v7.1.tgz
sudo cp cuda/include/cudnn.h /usr/local/cuda/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64/
sudo chmod a+r /usr/local/cuda/include/cudnn.h
sudo chmod a+r /usr/local/cuda/lib64/libcudnn*
```
* Verify
```
nvcc -V
```
## Install Caffe
## Install tensorflow-gpu
## Setup ladder
## 
