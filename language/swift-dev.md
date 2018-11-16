https://github.com/apple/swift

# System Requirements

sudo apt-get install git cmake ninja-build clang python uuid-dev libicu-dev icu-devtools libbsd-dev libedit-dev libxml2-dev libsqlite3-dev swig libpython-dev libncurses5-dev pkg-config libblocksruntime-dev


# Building Swift

A basic command to build Swift with optimizations and run basic tests with Ninja:
    utils/build-script -r -t

    frank@G470:~/git/swift/swift$ utils/build-script -r -t
    + mkdir -p /home/frank/git/swift/build/Ninja-RelWithDebInfoAssert
    + env HOST_VARIABLE_linux_x86_64__SWIFT_BENCHMARK_TARGETS= HOST_VARIABLE_linux_x86_64__SWIFT_RUN_BENCHMARK_TARGETS= HOST_VARIABLE_linux_x86_64__SWIFT_SDKS=LINUX HOST_VARIABLE_linux_x86_64__SWIFT_STDLIB_TARGETS=swift-test-stdlib-linux-x86_64 HOST_VARIABLE_linux_x86_64__SWIFT_TEST_TARGETS=check-swift-linux-x86_64 /home/frank/git/swift/swift/utils/build-script-impl --workspace /home/frank/git/swift --build-dir /home/frank/git/swift/build/Ninja-RelWithDebInfoAssert --install-prefix /usr --host-target linux-x86_64 --stdlib-deployment-targets linux-x86_64 --host-cc /usr/bin/clang --host-cxx /usr/bin/clang++ --darwin-xcrun-toolchain default --darwin-deployment-version-osx=10.9 --darwin-deployment-version-ios=7.0 --darwin-deployment-version-tvos=9.0 --darwin-deployment-version-watchos=2.0 --cmake /usr/bin/cmake --cmark-build-type RelWithDebInfo --llvm-build-type RelWithDebInfo --swift-build-type RelWithDebInfo --swift-stdlib-build-type RelWithDebInfo --lldb-build-type RelWithDebInfo --foundation-build-type RelWithDebInfo --llvm-enable-assertions true --swift-enable-assertions true --swift-stdlib-enable-assertions true --swift-analyze-code-coverage false --cmake-generator Ninja --build-jobs 4 '--common-cmake-options=-G Ninja -DCMAKE_C_COMPILER:PATH=/usr/bin/clang -DCMAKE_CXX_COMPILER:PATH=/usr/bin/clang++' --build-args=-j4 --build-stdlib-deployment-targets all --ninja-bin=/usr/bin/ninja --skip-build-foundation --skip-build-xctest --skip-build-lldb --skip-build-llbuild --skip-build-libdispatch --skip-build-swiftpm --skip-build-ios-device --skip-build-ios-simulator --skip-build-tvos-device --skip-build-tvos-simulator --skip-build-watchos-device --skip-build-watchos-simulator --skip-build-android --skip-test-ios-host --skip-test-ios-simulator --skip-test-tvos-host --skip-test-tvos-simulator --skip-test-watchos-host --skip-test-watchos-simulator --skip-test-android-host --skip-test-benchmarks --skip-test-optimized
    Couldn't find cmark source directory.
    utils/build-script: fatal error: command terminated with a non-zero exit status 1, aborting


http://weibo.com/2277420203/Dthwa9h73?sudaref=www.baidu.com&retcode=6102&type=comment
    吕文翰_JohnLui
   4月30日 02:33 来自 iPhone 6
   用 Ubuntu 16.04 LTS 编译 Swift 是一种怎样的体验？16G 内存耗尽，外加 5G swap，才能编译成功，如果 swap 不在 SSD 上趁早强制关机……
