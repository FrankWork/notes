https://swift.org/download/#using-downloads

# Swift REPL
------------------------------------

:type lookup Glibc








# Install
------------------------------------
Requirements
	Ubuntu 14.04 or 15.10 (64-bit)
Supported Target Platforms
	Ubuntu 14.04 or 15.10 (64-bit)


## 1. Install required dependencies:
	$ sudo apt-get install clang libicu-dev

## 2. Download the latest binary release above.

The swift-<VERSION>-<PLATFORM>.tar.gz file is the toolchain itself. The .sig file is the digital signature.

If you are downloading Swift packages for the first time, import the PGP keys into your keyring:

$ gpg --keyserver hkp://pool.sks-keyservers.net \
      --recv-keys \
      '7463 A81A 4B2E EA1B 551F  FBCF D441 C977 412B 37AD' \
      '1BE1 E29A 084C B305 F397  D62A 9F59 7F4D 21A5 6D5F'
or:

$ wget -q -O - https://swift.org/keys/all-keys.asc | gpg --import -
Skip this step if you have imported the keys in the past.

Verify the PGP signature.

The .tar.gz archives for Linux are signed using GnuPG with one of the keys of the Swift open source project. Everyone is strongly encouraged to verify the signatures before using the software.

First, refresh the keys to download new key revocation certificates, if any are available:

$ gpg --keyserver hkp://pool.sks-keyservers.net --refresh-keys Swift
Then, use the signature file to verify that the archive is intact:

$ gpg --verify swift-<VERSION>-<PLATFORM>.tar.gz.sig
...
gpg: Good signature from "Swift Automatic Signing Key #1 <swift-infrastructure@swift.org>"
If gpg fails to verify because you don’t have the public key (gpg: Can't check signature: No public key), please follow the instructions in Active Signing Keys below to import the keys into your keyring.

You might see a warning:

gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
This warning means that there is no path in the Web of Trust between this key and you. The warning is harmless as long as you have followed the steps above to retrieve the key from a trusted source.

If gpg fails to verify and reports “BAD signature”, do not use the downloaded toolchain. Instead, please email swift-infrastructure@swift.org with as much detail as possible, so that we can investigate the problem.
Extract the archive with the following command:

## 3. tar

$ tar xzf swift-<VERSION>-<PLATFORM>.tar.gz
This creates a usr/ directory in the location of the archive.

Add the Swift toolchain to your path as follows:

## 4. PATH

$ export PATH=/home/frank/bin/swift-2.2.1-RELEASE-ubuntu14.04/usr/bin:"${PATH}"
$ export TOOLCHAINS=$SWIFT_PATH

You can now execute the swift command to run the REPL or build Swift projects.

Active Signing Keys
The Swift project uses one set of keys for snapshot builds, and separate keys for every official release. We are using 4096-bit RSA keys.

The following keys are being used to sign toolchain packages:

Swift Automatic Signing Key #1 <swift-infrastructure@swift.org>

Downloadhttps://swift.org/keys/automatic-signing-key-1.ascFingerprint7463 A81A 4B2E EA1B 551F FBCF D441 C977 412B 37ADLong IDD441C977412B37AD
To import the key, run:

$ gpg --keyserver hkp://pool.sks-keyservers.net \
      --recv-keys \
      '7463 A81A 4B2E EA1B 551F  FBCF D441 C977 412B 37AD'
Or:

$ wget -q -O - https://swift.org/keys/automatic-signing-key-1.asc | gpg --import -
Swift 2.2 Release Signing Key <swift-infrastructure@swift.org>

Downloadhttps://swift.org/keys/release-key-swift-2.2.ascFingerprint1BE1 E29A 084C B305 F397 D62A 9F59 7F4D 21A5 6D5FLong ID9F597F4D21A56D5F
To import the key, run:

$ gpg --keyserver hkp://pool.sks-keyservers.net \
      --recv-keys \
      '1BE1 E29A 084C B305 F397  D62A 9F59 7F4D 21A5 6D5F'
Or:

$ wget -q -O - https://swift.org/keys/release-key-swift-2.2.asc | gpg --import -

You can verify that you are running the expected version of Swift by entering the swift command and passing the --version flag:

https://swift.org/getting-started/#using-the-repl

$ swift --version
Swift version 2.2.1 (swift-2.2.1-RELEASE)
Target: x86_64-unknown-linux-gnu

$ swiftc test.swift


#swift build
----------------------------------
$ mkdir Hello
$ cd Hello
$ touch Package.swift
$ mkdir Sources
$ touch Sources/main.swift
$ # write your code
$ swift build
$ .build/debug/Hello


# Swift Version Info
------------------------------------
$ swift --version
	Swift version 3.0 (swift-3.0-PREVIEW-1)
	Target: x86_64-unknown-linux-gnu
$ swiftc --version
	Swift version 3.0 (swift-3.0-PREVIEW-1)
	Target: x86_64-unknown-linux-gnu
$ swift build --version
	Swift Package Manager – Swift 3.0
$ swift package --version
	Swift Package Manager – Swift 3.0
	
	
	
	
