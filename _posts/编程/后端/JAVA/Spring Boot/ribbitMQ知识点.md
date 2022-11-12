### boot整合ribbitMQ

#### 创建RibbitMQ运行环境

```js
1.安装erlang环境
链接 https://www.erlang.org/downloads   别忘记配置环境变量
2.安装RibbitMQ
链接 https://www.rabbitmq.com/install-windows.html#installer   网络不是很好

装完RibbitMQ之后  打开 安装目录\\rabbitmq_server-3.9.14\sbin  运行以下cmd命令
rabbitmq-plugins enable rabbitmq_management
双击该目录下的  rabbitmq-service.bat  重启服务即可

安装教程 https://blog.csdn.net/qq_47588845/article/details/107986373
对应关系 https://www.rabbitmq.com/which-erlang.html
```

#### 引入依赖

```js
<!--rabbitmq-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

#### yml文件

```yaml
server:
  port: 8021
spring:
  #给项目来个名字
  application:
    name: rabbitmq-provider
  #配置rabbitMq 服务器
  rabbitmq:
    host: 127.0.0.1
    port: 5672
    username: root
    password: root
    #虚拟host 可以不设置,使用server默认host
    virtual-host: JCcccHost
```

