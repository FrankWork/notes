```bash
$ sudo apt-get install autoconf automake libtool curl make g++ unzip
$ wget https://github.com/google/protobuf/releases/download/v3.5.1/protobuf-cpp-3.5.1.tar.gz

$ ./configure --prefix=/usr/local
$ make
$ make check
$ sudo make install
$ sudo ldconfig # refresh shared library cache.


c++ my_program.cc my_proto.pb.cc `pkg-config --cflags --libs protobuf`

or configure CXXFLAGS="$(pkg-config --cflags protobuf)" \
          LIBS="$(pkg-config --libs protobuf)"
```