## kiss gate

- kiss/net 网关，反代 tcp、websocket 协议到后端 tcp 线路，

- 支持负载均衡、realip


## 安装

- go get github.com/nothollyhigh/kissgate


## 运行

- kissgate -config="config.xml"


## 配置

```xml
<setting>
    <!-- debug: 设置日志是否输出到控制台 -->
    <!-- logdir: 日志目录 -->
    <!-- redirect: 是否开启全局tcp重定向 -->
    <options debug="true" logdir="./logs/" redirect="true">
        <heartbeat interval="60" timeout="50"/>
    </options>

    <proxy>
        <!-- tcp 10000 端口 反代到 tcp 10001 10002 端口 -->
        <line name="tcp" addr=":10000" type="tcp">
            <node addr="127.0.0.1:10001" maxload="50000"/>
            <node addr="127.0.0.1:10002" maxload="50000"/>
        </line>

        <!-- websocket 20000 端口, 路由 /gate/ws, 反代到 tcp 20001 20002 端口 -->
        <line name="ws" addr=":20000" type="websocket" tls="false">
            <route path="/gate/ws"/>
            <node addr="127.0.0.1:20001" maxload="50000"/>
            <node addr="127.0.0.1:20002" maxload="50000"/>
        </line>
    </proxy>
</setting>
```
