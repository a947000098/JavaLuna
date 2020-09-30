先随意登上一个机器

命令： telnet ip 20881

命令：ls 查看你请求机器工程的dubbo接口

命令：invoke + 你的接口（参数）

比如：invoke com.bee.api.service.CustomerActivityService.batchQueryScoreNoOrder({"activity":1.0,"limit":10,"beginTime":1594396800000,"endTime":1594479600000} )