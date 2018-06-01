# May_SQLAlert_Rule_Release

1. 概览
五月份计划发布sqlalert规则6条,如下：
iTAP层数据监控：
    索引内有无数据规则  ---  alert/itap/nodta-index.rule
    L2层有无数据规则  ---  alert/itap/nodata-link.rule
    TCP扫描规则 ---  alert/tcp/flows/syn-sip.rule
    HTTP错误规则 ---  alert/http/status/sip.rule
    HTTP延迟规则 ---  alert/http/latency/sip.rule
    DNS错误规则  --- alert/dns/status/sip.rule
以上task已经在 rules/tasks/alert-client-base.json 配置中添加

2. 安装及运行

2.1 无需要安装，使用如下命令解压后即可使用
      tar -zxvf sqlalert-1.0.4
      cd sqlalert-1.0.4


2.2 目录说明
      ./bin     - 为 sqlalert 可执行文件目录
      ./rules  - 为规则库目录，即 sqlalert 的运行目录


2.3 配置
      2.3.1 全局配置 rules/globals/sys.rule：
             __sys_lang__ = "cn";                    配置语言环境。
             __es_host__ = "localhost:9200";      配置 ES 集群地址及端口号
             __enable_alert_xxx__ = true/false;    配置输出项
      
      
      2.3.2 规则配置
      修改，添加 需要监控的itap服务器名称 (itap名称可在运行itap机器的/usr/local/info/desc_nodeinfo.json 获得)
          ./rules/alert/itap/cfg/cn/nodata-index.rule 或 ./rules/alert/itap/cfg/en/nodata-index.rule
          ./rules/alert/itap/cfg/cn/nodata-link.rule 或 ./rules/alert/itap/cfg/en/nodata-link.rule
      修改变量
          __itaplist__
          __itapdict__
          
          
      2.3.3 如需要修改规则参数，请到 ./rules/alert/ 对应的目录下进行修改
           ./rules/alert/<proto>/<type>/<name>.rule
      用 HTTP 延迟规则为例（其他规则类似）
            规则文件为:  ./rules/alert/http/latency/sip.rule
            中文配置文件: ./rules/alert/http/latency/cfg/cn/sip.rule
            英文配置文件: ./rules/alert/http/latency/cfg/en/sip.rule
            
            
      2.4 运行规则库  
      运行规则前，请确认配置好了ES地址; 如果要运行监控数据那些规则请确认itap名称是填写正确
            cd sqlalert-1.0.4
            ./bin/sqlalert --etc ./rules --task tasks/alert-client-base.json


