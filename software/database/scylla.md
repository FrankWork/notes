C++ Cassandra

```bash
git clone https://github.com/scylladb/scylla.git
cd scylla
git submodule update --init --recursive
sudo ./install-dependencies.sh

./configure.py --mode=release

ninja-build -j8
./build/release/scylla

./build/release/scylla --datadir tmp --commitlog-directory tmp --smp 1
./build/release/scylla --help
```
