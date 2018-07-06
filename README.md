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
## Install ZBar
```
sudo apt-get install libzbar-dev libzbar0
```
* Install pyzbar
The official version of ZBar does not support Python 3. So we recommend using pyzbar which supports both ython 2 and Python 3. If you just want to work with python 2, you can install zbar and skip installing pyzbar.

Install ZBar (NOTE: Official zbar version does not support Python 3)
  ```
  pip install zbar
  ```
Install pyzbar
```
pip install pyzbar
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

* Install Asus Xtion2 Driver
```
sudo sh install.sh
```
* Set bandwith for USB2.0
```
sudo rmmod uvcvideo
sudo modprobe uvcvideo quirks=640
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
* Install Dependencies
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install -y build-essential cmake git pkg-config
sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install -y libatlas-base-dev
sudo apt-get install -y --no-install-recommends libboost-all-dev
sudo apt-get install -y libgflags-dev libgoogle-glog-dev liblmdb-dev
sudo apt-get install -y python-pip
sudo apt-get install -y python-dev
sudo apt-get install -y python-numpy python-scipy
sudo apt-get install -y libopencv-dev
```
* Download the source file from github
```
git clone https://github.com/BVLC/caffe.git
cp Makefile.config.example Makefile.config
```
* Install
```
cd python
pip install --upgrade pip
```
* fix the bug for pip 10.0
```
gvim /usr/bin/pip
from pip import __main__
if __name__ == '__main__':
    sys.exit(__main__._main())
```
```
for req in $(cat requirements.txt); do sudo pip install $req; done
```
open Makefile.config, locate line containing LIBRARY_DIRS and append /usr/lib/x86_64-linux-gnu/hdf5/serial
locate INCLUDE_DIRS and append /usr/include/hdf5/serial/

uncomment OPENCV_VERSION := 3

```
make all -j8
make test -j8
make runtest -j8
make pycaffe
export PYTHONPATH=/path/to/caffe/python:$PYTHONPATH
```
## Install tensorflow-gpu
Visit the website https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/
Download cuda-license-9-0_9.0.176-1_amd64.deb
```
sudo dpkg -i cuda-license-9-0_9.0.176-1_amd64.deb
```
Download cuda-misc-headers-9-0_9.0.176-1_amd64.deb
```
sudo dpkg -i cuda-misc-headers-9-0_9.0.176-1_amd64.deb
```
Download cuda-core-9-0_9.0.176.3-1_amd64.deb
```
sudo dpkg -i cuda-core-9-0_9.0.176.3-1_amd64.deb
```
Download cuda-cudart-9-0_9.0.176-1_amd64.deb
```
sudo dpkg -i cuda-cudart-9-0_9.0.176-1_amd64.deb
```
Download cuda-driver-dev-9-0_9.0.176-1_amd64.deb
```
sudo dpkg -i cuda-driver-dev-9-0_9.0.176-1_amd64.deb
```
Download cuda-cudart-dev-9-0_9.0.176-1_amd64.deb
```
sudo dpkg -i cuda-cudart-dev-9-0_9.0.176-1_amd64.deb
```
Download cuda-command-line-tools-9-0_9.0.176-1_amd64.deb
```
sudo dpkg -i cuda-command-line-tools-9-0_9.0.176-1_amd64.deb
```
git clone https://github.com/tensorflow/tensorflow
* Install Bazel
```
sudo apt-get install openjdk-8-jdk
echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list
curl https://bazel.build/bazel-release.pub.gpg | sudo apt-key add -
sudo apt-get update && sudo apt-get install bazel
sudo apt-get upgrade bazel
```
* Install Tensorflow Python Dependencies
```
sudo apt-get install python-numpy python-dev python-pip python-wheel
sudo pip install mock
```
* Install GPU prerequisites
```
 sudo apt-get install libcupti-dev
```
* Configure the installation
```
cd tensorflow
./configure
```
* Build pip package
To build a pip package for TensorFlow with GPU support, invoke the following command:
```
bazel build --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package
```
The bazel build command builds a script named build_pip_package. Running this script as follows will build a .whl file within the /tmp/tensorflow_pkg directory:
```
bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
```
* Install pip package
```
sudo pip install /tmp/tensorflow_pkg/tensorflow-1.8.0-py2-none-any.whl
```
## Setup ladder
* Download latest shadowsock-qt5-*.AppImage
```
https://github.com/shadowsocks/shadowsocks-qt5/releases
```
* Setup Auto Start
```
gnome-session-properties
```
add the downloaded shadowsocks-qt5-*.AppImage
* Install genpac
```
sudo apt-get install genpac
```
* Generate pac file
```
genpac --proxy="SOCKS5 127.0.0.1:1080" --gfwlist-proxy="SOCKS5 127.0.0.1:1080" -o autoproxy.pac --gfwlist-url="https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt"
```
* Setup system proxy
```
System settings -> Network -> Network Proxy -> Method (Automatic) -> Drag the generated file 
```
## 
