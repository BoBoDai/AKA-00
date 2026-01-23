1. 连接网络
方式一、通过wifi直接连接网络

方式二、在win上，通过usb共享网络之后进行一些配置
```shell
ip addr flush dev usb0
ip addr add 192.168.137.100/24 dev usb0
ip link set usb0 up

ip route del default
ip route add default via 192.168.137.1

echo "nameserver 8.8.8.8" > /etc/resolv.conf
```

2. 安装依赖

```python
pip install -r requirements.txt
```

5. 运行程序

```python
python3 car_control_server.py
```

后台启动##
```python
nohup python3 car_control_server.py > app.log 2>&1 &
```

6. 开机自启动脚本

在 /etc/init.d下新建配置文件 S99appinit

输入

```shell

```

6. mDNS配置
sg2002 内置支持了avahi，用
```shell
ps | grep avahi
```
可以发现
```shell
470 avahi avahi-daemon: running [licheervnano-366e.local]
```
为
<主机名>-<冲突后缀>.local

修改 /etc/hosts和 /etc/hostname

修改/etc/avahi/下的
avahi-daemon.conf

之后kill avahi的pid
之后 avahi-daemon -D

7. 生成证书
```shell
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 3650 -nodes
```

# 无交互生成自签名证书，有效期10年（3650天）
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 3650 -nodes -subj "/C=CN/ST=Beijing/L=Beijing/O=MyOrg/OU=MyDept/CN=localhost"

