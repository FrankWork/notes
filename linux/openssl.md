1.首先要生成服务器端的私钥(key文件):
openssl genrsa -des3 -out server.key 1024
运行时会提示输入密码,此密码用于加密key文件(参数des3便是指加密算法,当然也可以选用其他你认为安全的算法.),以后每当需读取此文件(通过openssl提供的命令或API)都需输入口令.如果觉得不方便,也可以去除这个口令,但一定要采取其他的保护措施!
去除key文件口令的命令:
openssl rsa -in server.key -out server.key
