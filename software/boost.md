# install

```bash
$ wget https://dl.bintray.com/boostorg/release/1.66.0/source/boost_1_66_0.tar.bz2
$ tar --bzip2 -xf /path/to/boost_1_66_0.tar.bz2
$ cd path/to/boost_1_66_0
$ ./bootstrap.sh --help
$ ./bootstrap.sh --prefix=path/to/installation/prefix
$ ./b2 install

boost_1_66_0/ .................The “boost root directory”
   index.htm .........A copy of www.boost.org starts here
   boost/ .........................All Boost Header files
    
   libs/ ............Tests, .cpps, docs, etc., by library
     index.html ........Library documentation starts here
     algorithm/
     any/
     array/
                     …more libraries…
   status/ .........................Boost-wide test suite
   tools/ ...........Utilities, e.g. Boost.Build, quickbook, bcp
   more/ ..........................Policy documents, etc.
   doc/ ...............A subset of all Boost library docs

```

# path

Try setting `C_INCLUDE_PATH` (for C header files) or `CPLUS_INCLUDE_PATH` (for C++ header files).

```bash
$ export BOOST_ROOT=$HOME/bin/boost
$ export CPLUS_INCLUDE_PATH=$CPLUS_INCLUDE_PATH:$BOOST_ROOT/include
```

# test

```c++
#include <boost/lambda/lambda.hpp>
#include <iostream>
#include <iterator>
#include <algorithm>

int main()
{
    using namespace boost::lambda;
    typedef std::istream_iterator<int> in;

    std::for_each(
        in(std::cin), in(), std::cout << (_1 * 3) << " " );
}
```

```c++
$ g++ -I path/to/boost_1_66_0 example.cpp -o example
$ echo 1 2 3 | ./example
```