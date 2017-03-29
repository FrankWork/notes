Protol Buffers [https://developers.google.com/protocol-buffers/]

# Install

tools:

    autoconf
    automake
    libtool
    curl (used to download gmock)
    make
    g++
    unzip

$ sudo apt-get install autoconf automake libtool curl make g++ unzip
$ git clone https://github.com/google/protobuf.git

If you get the source from github, you need to generate the configure script first:

$ ./autogen.sh

By default, the package will be installed to /usr/local

$ make clean # build again
$ ./configure 
bash: ./configure: 没有那个文件或目录
$ make
$ make check
$ sudo make install
$ sudo ldconfig # refresh shared library cache.



