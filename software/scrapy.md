#Scrapy

##安装Scrapy

按照官方文档的说明，安装scrapy 需要以下程序或者库：
（1）、Python 2.7
（2）、lxml。 Most linux distributions ships PRepackaged versions of lxml. Otherwise refer tohttp://lxml.de/installation.html
（3）、OpenSSL。 This comes preinstalled in all Operating systems except Windows (see Platform specific installation notes)
（4）、pip or easy_install Python package managers
我们安装的Ubuntu14.01系统都已经自带了前面3个，Python的版本为2.7.6。为了验证是否有安装，我们来查看一下。
打开终端，执行如下命令python， 接下来就是import lxml， import OpenSSL。如下图。如果import没有报错，说明系统已经自带了。

为了能够保证下面的安装能够成功。我们先执行：sudo apt-get install python-dev
再执行：sudo apt-get install libevent-dev。
在这里说明一下，不安装上面两个可能会出现一些错误，导致在后面的工作无法进行。
接下来就是安装pip了，执行：sudo apt-get install python-pip。

最后，也就是最重要的，安装Scrapy。执行：
	$ sudo pip install Scrapy
或
	$ sudo apt-get install python-scrapy (自动解决依赖库,don't use it, the version is too old.)


安装pip
	wget https://raw.github.com/pypa/pip/master/contrib/get-pip.py
	sudo python get-pip.py

	pip install redis （推荐）

##Scrapy命令
1. runspider
	scrapy runspider stackoverflow_spider.py -o top-stackoverflow-questions.json
2. startproject
	scrapy startproject tutorial
3. crawl
	scrapy crawl dmoz
4. shell
	scrapy shell "http://www.baidu.com/"
5. storage
	scrapy crawl dmoz -o items.json
6. 路径
	/usr/local/lib/python2.7/dist-packages/scrapy/
7. 去重
	Bloom Filter算法，Berkeley DB， Redis
8. JOBDIR
	scrapy crawl sdustlink2 -s JOBDIR=crawls/sdustlink2
DoubanmoivePipeline
DoubanmoviePipeline

$ scrapy shell 'http://www.sdust.edu.cn' --nolog
>>> data = response.xpath('//*[@href]').extract()
>>>for item in data:
...     file.write('%s\n' % item.encode('utf-8'))
...
>>> file.close()
	>>> response.headers
{   'Date'      :   ['Tue, 08 Mar 2016 08:25:47 GMT'],
	'X-Powered-By':     ['PHP/5.2.6'],
	'Content-Type' :    ['text/html; charset=utf-8'],
	'Server'        :   ['Apache/2.2.3 (Red Hat)']
}

http://doc.scrapy.org/en/1.0/ 官方文档，
Built with Sphinx using a theme provided by Read the Docs.




















