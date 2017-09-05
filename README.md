# WechatBot
WechatBot python2.7

### 问题总结
* 1.特定成员信息转发
```
#coding=utf-8
from wxpy import *

bot = Bot()

# 定位群聊
company_group = ensure_one(bot.groups().search('test'))

# 定位成员 昵称不能带有空格
boss = ensure_one(company_group.search('Han.'))



# 将指定对象的消息转发到文件传输助手，消息前缀在2.7版本需要加上**u**
@bot.register(company_group)
def forward_boss_message(msg):
    if msg.member == boss:
        msg.forward(bot.file_helper, prefix=u'测试')

# 堵塞线程
embed()
```
* 2.特定消息频率检测
```
#coding:utf-8

import wxpy
from wxpy import *


bot = Bot('test.pkl')

def action():
    bot.file_helper.send()



#执行检测
result = detect_freq_limit(action)

#查看结果
print(result)
'''
返回的结果为(限制频率，限制周期)
