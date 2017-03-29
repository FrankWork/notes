印象笔记 Python SDK 快速入门指南
https://dev.yinxiang.com/doc/start/python.php

#0
下面是你的 API Key信息

它包含两部分 Consumer Key和Consumer Secret. 请务必保存好你的Consumer Secret并且不要泄漏给其他人。

Consumer Key: 1217077212
Consumer Secret: c5b26743b2edfc9f
这些信息会马上发送至你的邮箱。

你的印象笔记 API Key 现在已经在我们的开发环境 https://sandbox.evernote.com 中激活, 用于 测试和创建你的应用。

你的 key 没有 在“真实”的印象笔记服务https://app.yinxiang.com 中启用。当你的应用已经沙箱环境测试完毕准备发布的时候，请在此提交产品环境下API Key的激活申请。

#1
wget https://raw.github.com/pypa/pip/master/contrib/get-pip.py
sudo python get-pip.py
sudo pip install evernote
python -c 'from evernote.api.client import EvernoteClient'
#2


