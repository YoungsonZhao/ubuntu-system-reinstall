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
4. zsh –version
5. sudo reboot
6. sudo chsh -s $(which zsh)
7. sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
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
