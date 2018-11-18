国际化
International Component for Unicode

```
wget http://download.icu-project.org/files/icu4c/60.2/icu4c-60_2-Fedora27-x64.tgz
```


```bash
$ export ICU_HOME=$HOME/bin/icu
$ export CPLUS_INCLUDE_PATH=$CPLUS_INCLUDE_PATH:$ICU_HOME/include
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ICU_HOME/lib
```
