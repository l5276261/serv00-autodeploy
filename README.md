# serv00自动化部署启动，保活，并且可发送消息到Telegram

## 利用github Action以及python脚本实现

## 🙏🙏🙏点个Star！！Star！！Star！！

###  将代码fork到你的仓库并运行的操作步骤

## (一). Fork 仓库

```
1、访问原始仓库页面： 打开你想要 fork 的 GitHub 仓库页面。
2、Fork 仓库 点击页面右上角的 "Fork" 按钮，将仓库 fork 到你的 GitHub 账户下。
```

## (二). 设置 GitHub Secrets

```
1、创建 Telegram Bot 【非必须】，如果没有配置此项 tg无法收到节点信息
    在 Telegram 中找到 @BotFather，创建一个新 Bot，并获取 API Token。 
    获取到你的 Chat ID 方法一，在一休技术交流群里发送/id@KinhRoBot获取，返回用户信息中的ID就是Chat ID
    获取到你的 Chat ID 方法二，可以通过向 Bot 发送一条消息，然后访问 https://api.telegram.org/bot<your_bot_token>/getUpdates 找到 Chat ID
```

### 配置 GitHub Secrets

```
1、转到你 fork 的仓库页面。
2、点击 Settings，然后在左侧菜单中选择 Secrets。
3、添加以下 secrets 名称：ENV_CONFIG (包含账号环境参数配置信息的 JSON 数据)。值为如下 【此值可不配置】，默认即可：
{
  "uuid_ports": [
    {"uuid": "cbbc53be-7436-4418-bbc7-0243d057bf7e", "port": 0},【可修改自己的uuid值，也可以不修改,port值默认即可】
    {"uuid": "5ccac840-3c3b-11ef-b292-005056c00008", "port": 0},
    {"uuid": "6adcae4e-16cc-443d-98c0-49f5c5dd46b9", "port": 0}
  ],
  "env_config": {
    "reset": 1,【是否需要重置环境】
    "node_num": 3,【开启节点个数，由于节点serv00端口限制，最多可设3个】
    "outo_npm_install": 1,【默认即可】
    "code_source_url": "git clone http://github.com/zjxde/serv00-ws",
    "kill_pid_path": "serv00",【默认即可】
    "nodejs_name": "index"【默认即可】

  }
}
5、添加以下 secrets 名称：USER_INFO(包含账号密码信息信息的 JSON 数据)。【必须配置】，例如：
{
  "tg_config": {
    "tg_bot_token": "【申请tg机器人的token】",
    "tg_chat_id": "【Chat ID】",
    "send_tg": 0 【是否需要发送节点信息到telegram】
  },
  "accounts": [    【ACCOUNT此项配置优先级比ENV_CONFIG要高,支持多个账号批量部署】
    {
      "username": "【用户名】",
      "password": "【密码】",
      "domain": "junx123.cloudns.ch",【你申请的域名】
      "pannelnum": 6,【你申请机器号】
      "cmd":"python restart 60",【必填 reset:重新初始化环境 keepalive:保活 restart:只重启 三种模式后面参数都可跟保活间隔时间】
      "uuid_ports":[],【可修改自己的uuid值，也可以不修改,port值默认即可】
      "env_config": {},
      "basepath": ""【默认即可：/home/XXX[用户名]/domains/XXX[域名]/app2/serv00-ws/】
    },
    {
      "username": "xxx",
      "password": "xxx",
      "domain": "xxx",
      "pannelnum": 6,
      "cmd":"python restart 60",
      "uuid_ports":[],
      "env_config": {},
      "basepath": ""

    }
  ]
}
```

## (三). 启动 GitHub Actions

```
1、配置 GitHub Actions
    》在你的 fork 仓库中，进入 Actions 页面。
    》如果 Actions 没有自动启用，点击 Enable GitHub Actions 按钮以激活它。
2、运行工作流 
    》GitHub Actions 将会根据你设置自动运行脚本。
    》如果需要手动触发，可以在 Actions 页面手动运行工作流。
3、工作流文件有 
    auto_deploy.yaml:一开始部署使用此任务
    auto_restart.yaml : 可自定义命令重启服务器 注使用该使用需要手动配置 secrets 名称为 CMD，值为 py restart 60【推荐】 ，后面
    的数值可按自己需求自行修改( 参数说明：reset:重新初始化环境 keepalive:保活 restart:只重启 三种模式后面参数都可跟保活间隔时间)
```

## (四).注意事项

```
1、保密性: Secrets 是敏感信息，请确保不要将它们泄露到公共代码库或未授权的人员。
2、更新和删除: 如果需要更新或删除 Secrets，可以通过仓库的 Secrets 页面进行管理。
3、通过以上步骤，你就可以成功将代码 fork 到你的仓库下并运行了。如果需要进一步的帮助或有其他问题，请随时告知！
```
