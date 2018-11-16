Download zsh with:

wget -O zsh.tar.gz https://sourceforge.net/projects/zsh/files/latest/download
mkdir zsh && tar -xvzf zsh.tar.gz -C zsh --strip-components 1
cd zsh

You can compile zsh yourself, for example:

./configure --prefix=$HOME
make
make install

and then start it explicitly, or programmatically from your current shell's startup file (put exec $HOME/bin/zsh -l in the right spot)