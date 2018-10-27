# v2ray-websocket-nginx-cloudflare-CDN
一个v2ray+websocket+nginx+cloudflare CDN的简单教程，人人为我，我为人人


首先根据下面这篇教程把证书及密钥弄弄好

https://toutyrater.github.io/advanced/tls.html

然后把我那三个配置文件，你自己改一改，改成自己的信息

我Ubuntu16.04下服务端配置文件在/etc/v2ray/config.json

nginx配置文件在/etc/nginx/default

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

