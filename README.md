# EMQ X Broker

*EMQ X* 是一款完全开源，高度可伸缩，高可用的分布式 MQTT 消息服务器，适用于 IoT、M2M 和移动应用程序，可处理千万级别的并发客户端。

从 3.0 版本开始，*EMQ X* 完整支持 MQTT V5.0 协议规范，向下兼容 MQTT V3.1 和 V3.1.1，并支持 MQTT-SN、CoAP、LwM2M、WebSocket 和 STOMP 等通信协议。EMQ X 3.0 单集群可支持千万级别的 MQTT 并发连接。

- 新功能的完整列表，请参阅 [EMQ X Release Notes](https://github.com/emqx/emqx/releases)。
- 获取更多信息，请访问 [EMQ X 官网](https://www.emqx.cn/)。




## 从源码构建


### Install [Erlang/OTP-R21.3](.\Read_erlang.md) and [rebar3](https://www.rebar3.org/docs/getting-started#section-installing-from-source)

## Build on Linux/Unix/Mac

```shell
git clone https://github.com/hqzzzz/emqx.git emqxd
cd emqxd
git checkout $(git describe --tags $(git rev-list --tags --max-count=1))
make
./_build/emqx/rel/emqx/bin/emqx console
```

### Build rpm or deb package on Linux
```shell
make emqx-pkg
ls _packages/emqx
```


### Build docker image
```shell
TARGET=emqx/emqx make docker
```


## 添加自定义插件


---
1. rebar.config -> deps 段落 添加依赖


```erl
{deps,
   [ ...,
     {emqx_backend_mysql, {git, "https://github.com/hqzzzz/emqx-backend-mysql.git", {branch, "v4.1"}}}
   ]
}

```
---
2. rebar.config -> relx 段落  添加

```erl
{relx,
    [...
    , ...
    , {release, {emqx, git_describe},
       [
         {emqx_backend_mysql, load},
       ]
      }
    ]
}
```

---
3. data/loaded_plugins
```erl
{emqx_backend_mysql, true}.
```


## MQTT 规范

你可以通过以下链接了解与查阅 MQTT 协议:

[MQTT Version 3.1.1](https://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html)

[MQTT Version 5.0](https://docs.oasis-open.org/mqtt/mqtt/v5.0/cs02/mqtt-v5.0-cs02.html)

[MQTT SN](http://mqtt.org/new/wp-content/uploads/2009/06/MQTT-SN_spec_v1.2.pdf)



## 开源许可

Apache License 2.0, 详见 [LICENSE](./LICENSE)。

# Author

EMQ X Team.
