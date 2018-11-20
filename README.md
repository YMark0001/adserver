# adserver
广告交易平台


## adserver::es
ES服务为nginx二次开发的web服务器，接收来自网站的http请求，对参数进行校验处理后重定向至ams服务器获取广告内容，返回广告显示的html
### module::lua
lua模块
###作用：接收来自网站/APP的http消息，对消息参数进行解析打包，重定向至show模块/click模块
### module::click
点击消息处理
###作用：接收来自lua模块的点击消息，解析参数后将信息传递到logwriter模块
### module::show
展示消息处理
###作用：接收来自lua模块的广告展示请求，解析参数，发起向ams服务发起广告获取请求，成功得到广告后将广告显示Log信息传递到logwriter模块
### module::logwriter
点击/展示LOG文件写入
###作用：循环检查log消息队列，对未写入log文件的消息进行落地
## adserver::ams
AMS服务接收来自es的广告请求后筛选广告匹配创意，组装模板后返回返回http消息值es

## adserver::cs
CS服务定时读取来自es的log数据（包括广告展示和广告点击），根据广告类型进行计费，统计广告主，广告计划，网站主，广告位等点击收费情况


## adserver::cc
CC服务定时读取CS服务产生的log数据，对各集群中的点击计费等数据进行汇总，生成当日报表数据。并更新数据库中广告主，网站主等相关数据项

## adserver::ufo
UFO为后台系统，提供广告主，网站主，系统管理等操作
