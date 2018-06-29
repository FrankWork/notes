sudo apt-add-repository ppa:fish-shell/release-2
sudo apt-get update
sudo apt-get install fish


wget https://github.com/fish-shell/fish-shell/releases/download/2.7.1/fish-2.7.1.tar.gz
./configure --prefix=$HOME
make; 
make install