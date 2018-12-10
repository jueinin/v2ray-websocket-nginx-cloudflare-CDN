# v2ray-websocket-nginx-cloudflare-CDN
一个v2ray+websocket+nginx+cloudflare CDN的简单教程，人人为我，我为人人
18.12.10更新：

配置文件升级4.0版本，做了一些小修改

首先根据下面这篇教程把证书及密钥弄弄好

https://toutyrater.github.io/advanced/tls.html

这篇教程基本上就是运行三个命令就行了

首先关闭nginx：systemctl stop nginx

curl  https://get.acme.sh | sh

上面这个命令会让你安装socat，安装一下。apt install socat

~/.acme.sh/acme.sh --issue -d mydomain.me --standalone -k ec-256

把上面命令的mydomain.me替换成你自己的域名，如果nginx已经关闭了，而且cloudflare添加了指向自己服务器ip的域名解析，并且没有点云朵，应该会提示安装成功了

然后执行这个  ~/.acme.sh/acme.sh --installcert -d mydomain.me --fullchainpath /etc/v2ray/v2ray.crt --keypath /etc/v2ray/v2ray.key --ecc

上面这个就是把证书文件换个位置，别忘了把mydomain.me换成自己的域名，这样证书就申请完成了

然后把我那三个配置文件，你自己改一改，改成自己的信息

我Ubuntu16.04下服务端配置文件在/etc/v2ray/config.json

nginx配置文件在/etc/nginx/sites-avaliable/default

记得申请证书的时候把apache卸载了，把nginx关闭掉，不然会报错，如果提前搞了cloud flare也关掉，还有配置文件修改完毕之后重启服务才能生效这个很关键的，不然看着配置文件累死都找不到毛病其实是配置文件没更新。。。。我就被这个坑撞的不要不要的

systemctl restart nginx;systemctl restart v2ray

确保一下输入https;//你的域名可以跑起来，这个很关键

三个文件弄好之后,如果ip没被墙就可以试着连接一下了，我觉得应该能连上的，不能连上欢迎提issue

这个时候呢如果能连上，可以开启一波cloud flare了。

这个东西会转发websocket流量，可以隐藏掉ip，我感觉基本上封也是封cloudflare的ip了  23333.。。

cloud flare好像要把那个ssl打开，websocket转发是默认打开的，别给关了。

一般没用cloud flare之前能连上用了之后应该也能连上；

有人说cloud flare是减速器有人说是加速器，反正在我机子上是加速器，感觉还可以，我的机子是最便宜最垃圾的ovz玩具机，以前直接装一个ssr到了晚高峰的时候大概只能跑1-5mbps，弄成v2ray加bbr加cdn之后能跑到三十mbps。。流畅1080p，不过他虽然网速还可以，但是是延迟还是什么原因浏览网页的时候会加载的相对慢一些，个人感觉可以接受

另外如果是ovz的机子想要装bbr，可以用仓库的那个bbr文件，南墙大佬写的，在此致谢。端口号填你服务端的端口号就行。








简洁版！！！
先去申请域名然后搞定cloud flare的域名解析，确保云朵没有点
apt update

curl  https://get.acme.sh | sh

apt install socat

~/.acme.sh/acme.sh --issue -d mydomain.me --standalone -k ec-256
我上下的两条命令记得域名换成自己的
~/.acme.sh/acme.sh --installcert -d mydomain.me --fullchainpath /etc/v2ray/v2ray.crt --keypath /etc/v2ray/v2ray.key --ecc

证书安装完成！

然后仓库三个配置文件复制一下，default文件改好之后放到/etc/nginx/sites-avaliable/default   服务端文件放在/etc/v2ray/config.json

都保存之后  systemctl restart nginx      systemctl restart v2ray

然后用客户端配置文件改一下，不出意外应该能连上了，连不上提issues

最后把cloud flare云朵点上去就可以开启cdn了

结束！




tips：
国内用cloud flare的话，一般是从新加坡的cf节点走的，没错，就是新加坡，不是大家常说的美国，所以完全可以买个新加坡的辣鸡机器，然后套CDN，高峰期延迟也就100-130的样子，我这边江苏移动，带宽能跑满。


