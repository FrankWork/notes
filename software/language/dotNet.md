https://www.microsoft.com/net/core#ubuntu


Install for Ubuntu 14.04

Add the new apt-get feed

$ sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
$ sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
$ sudo apt-get update

Install .NET Core SDK

$ sudo apt-get install dotnet-dev-1.0.0-preview1-002702
下列软件包有未满足的依赖关系：
 dotnet-dev-1.0.0-preview1-002702 : 依赖: dotnet-sharedframework-microsoft.netcore.app-1.0.0-rc2-3002702 但是它将不会被安装
E: 无法修正错误，因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系。

Install for Debian 8.2

Install .NET Core SDK

sudo apt-get install curl
curl -sSL https://raw.githubusercontent.com/dotnet/cli/rel/1.0.0/scripts/obtain/dotnet-install.sh | bash /dev/stdin --version 1.0.0-preview1-002702 --install-dir ~/bin/dotnet
sudo ln -s ~/bin/dotnet/dotnet ~/bin/dnet


输出：
dotnet-install: Downloading https://dotnetcli.blob.core.windows.net/dotnet/beta/Binaries/1.0.0-preview1-002702/dotnet-dev-ubuntu-x64.1.0.0-preview1-002702.tar.gz
dotnet-install: Extracting zip
dotnet-install: Adding to current process PATH: /home/frank/bin/dotnet. Note: This change will be visible only when sourcing script.
dotnet-install: Installation finished successfuly.


Initialize some code

$ mkdir hwapp
$ cd hwapp
$ dotnet new

Run the app

$ dotnet restore
$ dotnet run


安装 vs code 
https://code.visualstudio.com


# For .deb
sudo dpkg -i <file>.deb

# For .rpm (Fedora 21 and below)
sudo yum install <file>.rpm

# For .rpm (Fedora 22 and above)
sudo dnf install <file>.rpm






