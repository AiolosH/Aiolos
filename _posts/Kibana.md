---
title: kibana
description: 学
date: 2020-02-25 00:00:00 +08:00
tags: 学
category: 学
---

# kibana

### 下载 解压
> wget https://artifacts.elastic.co/downloads/kibana/kibana-6.3.2-linux-x86_64.tar.gz


### 修改配置
配置文件位置在config/kibana.yml

``` yml
# 访问端口
server.port: 5601

# 远程访问
server.host: "0.0.0.0"

# 使您能够指定如果您在代理后运行的 Kibana 的路径。这只影响 Kibana 生成的 URL，您的代理应该在转发请求到 Kibana 之前删除 basePath 值。此设置不能以斜杠（/）结尾。
#server.basePath: ""

# 默认值 : 1048576 传入服务器请求的最大有效负载大小（以字节为单位）。
#server.maxPayloadBytes: 1048576

# “your-hostname” 用于标识此 Kibana 实例的可读的显示名称。
#server.name: "your-hostname"

# Elasticsearch实例地址
#elasticsearch.url: "http://localhost:9200"

# 默认值 : true 当此设置的值为 true 时，Kibana 使用 server.host 设置中指定的主机名。当此设置的值为 false 时，Kibana 使用连接到此 Kibana 实例的主机的主机名。
#elasticsearch.preserveHost: true

# 默认值 : “.kibana”Kibana 使用 Elasticsearch 中的索引来存储保存的搜索，可视化和仪表板。如果索引不存在，Kibana 将创建一个新索引。
#kibana.index: ".kibana"

# 	默认值 : home 要加载的默认应用程序。
#kibana.defaultAppId: "home"

# 如果您的 Elasticsearch 受基本认证保护，这些设置提供 Kibana 服务器用于在启动时对 Kibana 索引执行维护的用户名和密码。您的 Kibana 用户仍需要使用通过 Kibana 服务器代理的 Elasticsearch 进行身份验证。
#elasticsearch.username: "user"
#elasticsearch.password: "pass"

# server 的SSL设置
#server.ssl.enabled: false
#server.ssl.certificate: /path/to/your/server.crt
#server.ssl.key: /path/to/your/server.key

# Elasticsearch 的SSL设置
#elasticsearch.ssl.certificate: /path/to/your/client.crt
#elasticsearch.ssl.key: /path/to/your/client.key
#elasticsearch.ssl.certificateAuthorities: [ "/path/to/your/CA.pem" ]
#elasticsearch.ssl.verificationMode: full

# pingElasticsearch超时时间
#elasticsearch.pingTimeout: 1500

# 读取Elasticsearch数据超时时间
#elasticsearch.requestTimeout: 30000

# 默认值 : [ 'authorization' ] 要发送到 Elasticsearch 的 Kibana 客户端头标列表。要发送任何客户端头，请将此值设置为 []（一个空列表）。
#elasticsearch.requestHeadersWhitelist: [ authorization ]

# 默认值 : {} 要发送到 Elasticsearch 的（header name）标题名称和值。不管如何配置 elasticsearch.requestHeadersWhitelist，任何自定义的 header 都不能被客户端头覆盖
#elasticsearch.customHeaders: {}

# Time in milliseconds for Elasticsearch to wait for responses from shards. Set to 0 to disable.
#elasticsearch.shardTimeout: 0

# Time in milliseconds to wait for Elasticsearch at Kibana startup before retrying.
#elasticsearch.startupTimeout: 5000

# Specifies the path where Kibana creates the process ID file.
#pid.file: /var/run/kibana.pid

# Enables you specify a file where Kibana stores log output.
#logging.dest: stdout

# Set the value of this setting to true to suppress all logging output.
#logging.silent: false

# Set the value of this setting to true to suppress all logging output other than error messages.
#logging.quiet: false

# Set the value of this setting to true to log all events, including system usage information
# and all requests.
#logging.verbose: false

# Set the interval in milliseconds to sample system and process performance
# metrics. Minimum is 100ms. Defaults to 5000.
#ops.interval: 5000

# The default locale. This locale can be used in certain circumstances to substitute any missing
# translations.
#i18n.defaultLocale: "en"
```