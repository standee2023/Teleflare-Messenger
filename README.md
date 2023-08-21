# Teleflare-Messenger
 Send Telegram bot messages with Cloudflare workers

## Usage

1. Create a cloudflare workers

2. Copy the code in workers.js to the workers

3. Fill in your Telegram Bot Token and your Chat ID

4. Send GET request to your workers URL 

    ```
    https://yourworkersname.yourcloudflarename.workers.dev/?title=Title&msg=test_message
    ```

**Note**: The script uses [MarkdownV2](https://core.telegram.org/bots/api#markdownv2-style) as default parse mode, if you want to use plain text or HTML, you need to modify the title bold symbol(**) at line 46.


一、创建 bot 以及获取 token

打开 BotFather
url: https://t.me/BotFather 打开与它的聊天界面，不论是 Windows mac 还是 Android iOS 的 telegram 客户端。

1.输入 /newbot 后回车

它会回你以下内容


Alright, a new bot. How are we going to call it? Please choose a name for your bot.


2.这个名字是显示名称 （display name）,不是唯一识别码，现在随便设置一下，之后可以通过 /setname 修改

比如设置成 Zhang san's sweety bot


3.接着会让你设置唯一名称。字符串必须 endsWith bot，比如 abc_bot 或 HelloWorldbot 都是合法的。如果你设置的名字已经被占用需要重新设置。比如你设置成了 test_bot


Good. Now let's choose a username for your bot. It must end in bot. Like this, for example: TetrisBot or tetris_bot.


4.恭喜！设置成功。会返回给你重要的 API token，务必要保存好它。另外你的 bot 的唯一 url 就已经生成: https://t.me/test_bot


Done! Congratulations on your new bot. You will find it at t.me/test_bot. You can now add a description, about section and profile picture for your bot, see /help for a list of commands. By the way, when you've finished creating your cool bot, ping our Bot Support if you want a better username for it. Just make sure the bot is fully operational before you do this.

Use this token to access the HTTP API:
 12345678:sdfsfadsfasdfasdfasdfgdfhdfghfgh
 Keep your token secure and store it safely, it can be used by anyone to control your bot.

For a description of the Bot API, see this page: https://core.telegram.org/bots/api


5.一些其他必要的命令
◦/setdescription 帮助你设置 bot 的描述
◦/setuserpic 设置 bot 的头像。上传的图片 size 需要大于等于 150x150。而且上传图片需要选择压缩，不能上传文件！

此时你的 bot 很快就可以使用了。


二、获取 chatId

观察这个 url https://api.telegram.org/bot{token}/getUpdates

1、使用第二步获得的 token 替换上述 url 中的 {token} 然后得到新的 url，复制粘贴到浏览器地址栏，回车请求。不出意外你会得到如下 response

{
    "ok": true,
    "result": []
}

很好。这时你打开你的 bot，随便和它说一句话，比如给它发一句 "Hello World"，然后重新请求一遍上述的 url（替换过 token 的），不出意外你收到的 response 是这样了


{
    "ok": true,
    "result": [
        {
            "update_id": 123456,
            "message": {
                "message_id": 56,
                "from": {
                    "id": 72384234234,
                    "is_bot": false,
                    "first_name": "sdfsdf",
                    "last_name": "sdfsdf",
                    "username": "sdfsdf",
                    "language_code": "en"
                },
                "chat": {
                    "id": 123456789,
                    "first_name": "sdfsdf",
                    "last_name": "sdfsdf",
                    "username": "sdfsdf",
                    "type": "private"
                },
                "date": 1212121212,
                "text": "/start",
                "entities": [
                    {
                        "offset": 0,
                        "length": 6,
                        "type": "bot_command"
                    }
                ]
            }
        },
        {
            "update_id": 123456,
            "message": {
                "message_id": 6,
                "from": {
                    "id": 23232323,
                    "is_bot": false,
                    "first_name": "sdfsdfsdf",
                    "last_name": "sdfsdfsdf",
                    "username": "sdfsdfsdf",
                    "language_code": "en"
                },
                "chat": {
                    "id": 123456,
                    "first_name": "sdfsdfsdf",
                    "last_name": "sdfsfdsdf",
                    "username": "sdfsdfsdf",
                    "type": "private"
                },
                "date": 1234567,
                "text": "Hello World"
            }
        }
    ]
}

2、如果浏览器没有安装一些 json 美化插件，会得到 json string 原文，那么复制它们到任何一个在线 json 解析格式化网站，比如 https://www.sojson.com/ 选择对应的格式化功能格式化文本。

其中的 result[0].message.chat.id 的值就是 chatId 也就是 123456789

知道了 token 和 chatId 就可以使用 bot 了。


