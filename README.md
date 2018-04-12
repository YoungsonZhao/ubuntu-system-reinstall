# ubuntu-system-reinstall
This is a manual that shows the detailed instructions to setup a development environment on Ubuntu 16.04 step by step.
## Setup Chinese Input Method
1. System Settings -> Language Support -> Update -> Install/Remove Languages -> Check Chinese
2. sudo apt-get install ibus ibus-clutter ibus-gtk ibus-gtk3 ibus-qt4
3. im-config -s ibus
4. sudo apt-get install ibus-pinyin
5. sudo reboot
6. sudo ibus-setup
