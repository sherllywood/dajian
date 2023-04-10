# 科学上网：VPS 搭建 X-UI 面板

## 使用X-UI搭建代理服务，具有以下优点：

- 支持系统状态监控：如CPU、内存、硬盘等状态
- 支持多用户多协议，网页可视化操作
- 支持流量统计
- 支持自定义Xray配置模板
- 支持HTTPS访问面板
- 支持面板自定义端口，账号与密码
- 快速生成分享连接或二维码
- 支持CDN套用
- 支持Fallback分流设置

## 准备工作

- 1、已经解析的域名，Win+R输入CMD 回车：键入ping 空格输入你的域名，检查一下是否可以ping通
- 2、一台境外VPS主流系统，例如：Debian/Ubuntu/CentOS
- 3、下载并安装FinalShell SSH工具

Windows版下载地址:
http://www.hostbuf.com/downloads/finalshell_install.exe

macOS版下载地址:
http://www.hostbuf.com/downloads/finalshell_install.pkg

## 安装更新运行环境

## 安装 X-ui 面板
### 申请 SSL 证书
下面环境的安装方式，大家根据自己的系统选择命令安装就好了。
### 1、Debian/Ubuntu系统执行以下命令：
     
    apt update -y && apt install -y curl && apt install -y socat
     
### 2、CentOS系统执行以下命令：

    yum update -y && yum update -y && yum install -y socat
    
    
    ### 放行80端口

        iptables -I INPUT -p tcp --dport 80 -j ACCEPT
        
### 放行443端口，把80改成443
        
        iptables -I INPUT -p tcp --dport 443 -j ACCEPT
        
        ### 放行9999端口
        
        iptables -I INPUT -p tcp --dport 9999 -j ACCEPT
    
### 运行Acme脚本

    curl https://get.acme.sh | sh
    
### 申请证书及密钥
【将代码中注释的邮箱和域名，改为你自己的】

    ~/.acme.sh/acme.sh --register-account -m 2100742336@qq.com
    
    
------------ 
 

    ~/.acme.sh/acme.sh  --issue -d 输入你的域名  --standalone
    
 ### 下载证书及密钥
 
    ~/.acme.sh/acme.sh --installcert -d 输入你的域名 --key-file /root/private.key --fullchain-file /root/cert.crt
    
### 安装&升级x-ui面板一键脚本

    bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
    ###安装xui
    admin账号 admin密码 登录
    访问：域名：9999端口（需放行）

私钥路径：/root/private.key

公钥路径：/root/cert.crt 

### ##BBR2加速##
本脚本建议在Debian≥9或是CentOS≥8以上的系统中使用

    wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
 
 
## 注意事项
- 1、如何在申请证书及密钥这一步搭建失败，检查并放行端口，口令如下：

### 放行80端口

        iptables -I INPUT -p tcp --dport 80 -j ACCEPT
        
### 放行443端口，把80改成443
        
        iptables -I INPUT -p tcp --dport 443 -j ACCEPT







查看已开放的端口

        firewall-cmd --list-ports
            
    
开放端口（开放后需要要重启防火墙才生效）

    firewall-cmd --zone=public --add-port=3338/tcp --permanent
    
重启防火墙

    firewall-cmd --reload
    
停止防火墙

    systemctl stop firewalld
    

- 2、如果是全新安装，默认网页端口为 54321，用户名和密码默认都是 admin ，
如何遇到打不开的情况，可能是端口没有放行，用【方法1】键入停止防火墙代码，或键入开放端口代码。

- 3、V2ray软件：设置——参数设置——V2rayN设置——Core类型改为Xray_Core




一键安装脚本：navie
wget -N https://gitlab.com/rwkgyg/naiveproxy-yg/raw/main/naiveproxy.sh && bash naiveproxy.sh

1、甲骨文官网：https://www.oracle.com/cn/cloud/free
2、Xshell官网：https://www.xshell.com/zh/
3、Namesilo.com官网：https://www.namesilo.com/
Centos root模式：sudo -i
4、Naive一键脚本：
wget -N https://gitlab.com/rwkgyg/naiveproxy-yg/raw/main/naiveproxy.sh && bash naiveproxy.sh
5、naive客户端下载：https://github.com/klzgrad/naiveproxy/releases
json文件配置:
{
  "listen": "socks://127.0.0.1:1080",
  "proxy": "https://user:pass@example.com"
}



搭建NaiveProxy VPS
官方项目地址：https://github.com/klzgrad/naiveproxy/wiki
购买服务器并解析域名（服务器用 ）20.04测试ok  
防火墙设置：
检查防火墙状态：ufw status
防火墙开启和关闭：ufw enable    #开启    ufw disable   #关闭
甲骨文用这个开启防火墙放行端口
iptables -I INPUT -p tcp --dport 80 -j ACCEPT
iptables -I INPUT -p tcp --dport 443 -j ACCEPT
iptables -I INPUT -p tcp --dport 999 -j ACCEPT

开启指定tcp或者udp端口：ufw allow 22/tcp
同时开启tcp与udp端口：ufw allow 80
删除端口：ufw delete allow 445
要使用这个命令放行端口

apt-get update
apt update -y && apt install -y curl && apt install -y socat 
 这些待用 

更新系统：
安装caddy和naive


编译安装命令三条：

1.    apt install golang-go -y
 2.    go install github.com/caddyserver/xcaddy/cmd/xcaddy@latest
********************************************
    运行第二条指令出错的，这个是解决方法。
ubantu下使用sudo apt install golang-go指令安装go环境，安装过程没有报错，在使用时无法识别指令。
原因：未完整安装go环境，使用apt安装的版本可能会比较老。
解决：
apt-get install software-properties-common

sudo add-apt-repository ppa:longsleep/golang-backports 

sudo apt-get update 

sudo apt-get install golang-go

测试：
go version

*************************************************
 3.  ~/go/bin/xcaddy build --with github.com/caddyserver/forwardproxy@caddy2=github.com/klzgrad/forwardproxy@naive


输入命令：ls 
 

修改权限 chmod 777 文件路径  /root  root 文件无法进入时用

创建Caddyfile（文件名要一样，区分大小写），并添加配置
caddy常用指令
前台运行caddy：./caddy run

ctrl+C退出

后台运行caddy：./caddy start
停止caddy：./caddy stop
重载配置：./caddy reload
下载naive客户端：
  https://github.com/klzgrad/naiveproxy/releases/latest  navie复制到v2ray 安装目录下

在root 文件夹下新建文件：

Caddyfile配置：

:443, naive.buliang0.tk #你的域名
tls example@example.com #你的邮箱
route {
 forward_proxy {
   basic_auth user pass #用户名和密码
   hide_ip
   hide_via
   probe_resistance
  }
 #支持多用户
 forward_proxy {
   basic_auth user2 pass2 #用户名和密码
   hide_ip
   hide_via
   probe_resistance
  }
 reverse_proxy  https://demo.cloudreve.org  { #伪装网址
   header_up  Host  {upstream_hostport}
   header_up  X-Forwarded-Host  {host}
  }
}

搜索网站cloudreve+login



****************************************************
客户端配置：

{
  "listen": "socks://127.0.0.1:1080",
  "proxy": "https://admin:123520@www.tik886.gq"
}


*********************************************************
1 apt-get update  
2  apt-get install wget  
3 wget --version



# 如果vps不能访问 raw.githubusercontent.com 推荐使用这个
wget --no-check-certificate -qO natcfg.sh https://www.arloor.com/sh/iptablesUtils/natcfg.sh && bash natcfg.sh

https://www.youtube.com/watch?v=DVZ1SWO9ofM


