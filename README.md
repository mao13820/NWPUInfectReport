# 西工大疫情填报github action版本

### 使用流程

1. 点击项目右上角的Fork，Fork此项目
2. 到自己Fork的项目点击Actions，如果未启用，需要手动启用，然后启用需要运行的Workflows
3. 到自己Fork的项目点击Setting→Secrets→New secrets
4. 填写Name，和Value，需要添加以下三个
    - xgd_username -> 学号
    - xgd_password -> 密码
    - Skey(可选) -> [https://cp.xuthus.cc/](https://cp.xuthus.cc/)申请，用于推送qq，或自行设置其他推送
5. 在"Actions"中的"run"下点击"Run workflow"即可手动执行签到，后续运行按照schedule，默认在每天9:00自动签到，可自行修改

### 推送可以设置的参数( Key/name(名称) --> Value(值) )：

Github Actions添加在Setting→Secrets→New secrets，腾讯云函数SCF设置在环境变量里

1. Key: SCKEY --> Value: [Server酱的推送SCKEY的值](http://sc.ftqq.com/)
2. Key: SCTKEY --> Value: [Server酱·Turbo版的推送SCTKEY的值](http://sct.ftqq.com/)
3. Key: Skey --> Value: [酷推调用代码Skey](https://cp.xuthus.cc/)
4. Key: Smode --> Value: 酷推的推送渠道，不设置默认send.可选参数(send,group,psend,pgroup,wx,tg,ww,ding)
5. Key: pushplus_token --> Value: [pushplus推送token](http://www.pushplus.plus/)
6. Key: pushplus_topic --> Value: pushplus一对多推送需要的"群组编码"，一对一推送不用管填了报错
7. Key: tg_token --> Value: Telegram bot的Token，Telegram机器人通知推送必填项
8. Key: tg_chatid --> Value: 接收通知消息的Telegram用户的id，Telegram机器人通知推送必填项
9. Key: tg_api_host --> Value: Telegram api自建的反向代理地址(不懂忽略此项)，默认tg官方api=api.telegram.org

PS:腾讯云函数SCF的默认无推送，需要推送的话需要将[pusher.py](https://github.com/mengshouer/CheckinBox/blob/master/pusher.py)内的内容直接复制到所需函数的代码最上方！！！

### 自动同步仓库设置
基础使用：
> 上游变动后pull插件会自动发起pr，在默认的配置文件中如果有冲突需要自行**手动**确认。

安装[pull插件](https://github.com/apps/pull)，然后设置生效的仓库并确认此项目已在pull插件的作用下
PS. 如果未设置pull.yml配置文件，则mergeMethod的规则默认为none(我也不清楚none的pr规则

高级使用：
> 强制远程分支覆盖自己的分支

1. 先完成基础使用后，在.github目录下(创建/修改)文件pull.yml
2. 参考[插件使用文档](https://github.com/wei/pull#advanced-setup-with-config)进行修改
PS.强制远程分支覆盖自己的分支只需要将mergeMethod的值修改为hardreset

