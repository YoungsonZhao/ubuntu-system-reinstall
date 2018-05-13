# ubuntu-system-reinstall
This is a manual that shows the detailed instructions to setup a development environment on Ubuntu 16.04 step by step.
## Setup Chinese Input Method
1. System Settings -> Language Support -> Update -> Install/Remove Languages -> Check Chinese
2. sudo apt-get install ibus ibus-clutter ibus-gtk ibus-gtk3 ibus-qt4
3. im-config -s ibus
4. sudo apt-get install ibus-pinyin
5. sudo reboot
6. sudo ibus-setup
## Install ZSH
1. sudo apt-get install git
2. sudo apt-get install curl
3. sudo apt-get install zsh
4. zsh -version
5. sudo reboot
6. sudo chsh -s $(which zsh)
7. sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
8. sudo reboot
## Install Tmux
1. sudo apt-get install tmux
## Install & Setup Gvim
1. sudo apt-get install vim-gtk
2. curl http://j.mp/spf13-vim3 -L -o - | sh
3. copy .vimrc .vimrc.local .vimrc.bundle .vimrc.before to Home directory
4. :PlugginInstall in Gvim
5. cd .vim/bundle/
6. git clone --recursive https://github.com/Valloric/YouCompleteMe.git
7. sudo./install.py –clang-completer
8. copy .ycm_extra_conf.py to .vim/bundle/YouCompleteMe/third_party/ycmd/cpp/ycm
## Install OpenCV 3.2.0
1. sudo apt-get install build-essential
2. sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
3. sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
4. cd ~/opencv-3.2.0
5. mkdir build
6. cd build
7. cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..
8. make -j7 # runs 7 jobs in parallel
9. sudo make install
## Install ros-kinetic
1. sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
2. sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
3. sudo apt-get update
4. sudo apt-get install ros-kinetic-desktop-full
5. sudo rosdep init
6. rosdep update
7. echo "source /opt/ros/kinetic/setup.zsh" >> ~/.zshrc
8. source ~/.zshrc
## Install Eigen-3.3.4
1. cd Eiigen-3.3.4
2. mkdir build
3. cd build
4. cmake ..
5. sudo make install
## Install Ceres-1.13
1. sudo apt-get install cmake
2. sudo apt-get install libgoogle-glog-dev
3. sudo apt-get install libatlas-base-dev
4. sudo apt-get install libsuitesparse-dev
5. cd Ceres-1.13
6. mkdir build
7. cd buid
8. cmake ..
9. make -j3
10. make test
11. make install
## Install Pylon
1. cd pylon-5.0.11*
2. sudo tar -C /opt -xzf pylonSDK*.tar.gz
## Install cpprest
1. git clone --recursive https://github.com/Microsoft/cpprestsdk.git
2. cd cpprestsdk && cd Release
3. midir build
4. cmake ..
5. make -j4
6. sudo make install
## Install Zeal
1. sudo add-apt-repository ppa:zeal-developers/ppa
2. sudo apt-get update
3. sudo apt-get install zeal
## Install SSH
1. sudo apt-get install ssh
## Install Google-Chrome
1. sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/
2. wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -
3. sudo apt-get update
4. sudo apt-get install google-chrome-stable
## Install shadowsocks-qt5
1. sudo add-apt-repository ppa:hzwhuang/ss-qt5
2. sudo apt-get update
3. sudo apt-get install shadowsocks-qt5
## Install Numpy
1. sudo apt-get install python-pip
2. pip install --upgrade pip
3. sudo pip install numpy
4. pip install numpy
## Install Cuda & Cudnn
## Install Caffe
## Install tensorflow-gpu
## Setup ladder
## 
