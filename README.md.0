### docker启动shadowsocks客户端

```javascript
echo "1" > /proc/sys/net/ipv4/ip_forward #开启路由转发
docker run -it --restart=always --name ss -d -p 8118:8118 \
    -p 1080:1080 -e SS_SERVER="x.x.x.x.com" \
    -e SS_SERVER_PORT=38843 -e SS_SERVER_PASSWD='mtUNEyoBMB' \
    -e ENCRYPT_METHOD='aes-256-cfb' -e SS_LOCAL_PORT=1080 \
    -v /etc/localtime:/etc/localtime \
    964973791/ss:1.0.0
```


### SSR搭建

```javascript
cd /root/.local/share && git clone https://github.com/luo964973791/shadowsocksr.git
cd shadowsocksr 
bash ssr.sh install
bash ssr.sh config   #更改SSR服务器IP,端口，可以参考config.json进行配置.
yum install privoxy -y
cat /etc/privoxy/config | grep -E "127.0.0.1:1080|0.0.0.0"
listen-address  0.0.0.0:8118
forward-socks5t   /               127.0.0.1:1080 .
systemctl start privoxy && systemctl enable privoxy
```


### 配置全局代理

```javascript
vi ~/.bashrc
export http_proxy=http://127.0.0.1:8118
export https_proxy=https://127.0.0.1:8118
```



### 验证

```javascript
#查看IP是否改变.
curl cip.cc --socks5 127.0.0.1:1080
#返回一大堆HTML 则说明正常
curl www.google.com
```

