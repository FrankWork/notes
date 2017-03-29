## online
pip install theano

## offline
pip download theano
tar zxvf Theano-0.9.0.tar.gz
pip install Theano-0.9.0.tar.gz

Problem occurred during compilation with the command line below:
/usr/bin/g++ -shared -g -march=corei7-avx -mcx16 -msahf -mno-movbe -maes -mpclmul -mpopcnt -mno-abm -mno-lwp -mno-fma -mno-fma4 -mno-xop -mno-bmi -mno-bmi2 -mno-tbm -mavx -mno-avx2 -msse4.2 -msse4.1 -mno-lzcnt -mno-rtm -mno-hle -mno-rdrnd -mno-f16c -mno-fsgsbase -mno-rdseed -mno-prfchw -mno-adx -mfxsr -mxsave -mxsaveopt -mno-pku --param l1-cache-size=32 --param l1-cache-line-size=64 --param l2-cache-size=15360 -mtune=corei7-avx -DNPY_NO_DEPRECATED_API=NPY_1_7_API_VERSION -m64 -fPIC -I/home/liuzhihui/bin/python3.6/lib/python3.6/site-packages/numpy/core/include -I/home/liuzhihui/bin/python3.6/include/python3.6m -I/home/liuzhihui/bin/python3.6/lib/python3.6/site-packages/theano/gof -L/home/liuzhihui/bin/lib -L/home/liuzhihui/bin/python3.6/lib -fvisibility=hidden -o /home/liuzhihui/.theano/compiledir_Linux-3.10-el7.x86_64-x86_64-with-centos-7.2.1511-Core-x86_64-3.6.0-64/lazylinker_ext/lazylinker_ext.so /home/liuzhihui/.theano/compiledir_Linux-3.10-el7.x86_64-x86_64-with-centos-7.2.1511-Core-x86_64-3.6.0-64/lazylinker_ext/mod.cpp -lpython3.6m
/usr/bin/ld: /home/liuzhihui/bin/python3.6/lib/libpython3.6m.a(abstract.o): relocation R_X86_64_32S against `_Py_NotImplementedStruct' can not be used when making a shared object; recompile with -fPIC


$ CXXFLAGS="-fPIC"

