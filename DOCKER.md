## 安装与使用
首先安装docker和docker-compose,并且确保80 443端口未被占用(关闭nginx apache之类的,使用netstat -lnp查看),关闭cf云朵
### 安装BBR加速
bbr脚本在[这里](https://github.com/chiakge/Linux-NetSpeed),建议装BBR PLUS,用着还行,安装BBRplus的时候可能会提示是否删除其余内核,选否,重启即可.建议先安装BBR加速,因为安装完了需要重启才行
- 安装docker
    - curl -fsSL https://get.docker.com -o get-docker.sh
    - sh get-docker.sh
- 安装docker-compose
    - curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-Linux-x86_64" -o /usr/local/bin/docker-compose
    - chmod +x /usr/local/bin/docker-compose
- 安装git
    - apt install git -y
`git clone https://github.com/jueinin/v2ray-websocket-nginx-cloudflare-CDN.git`  
`cd v2ray-websocket-nginx-cloudflare-CDN/v2`   
 然后编辑Dockerfile-main,修改$V2RAY_DOMAIN为你的域名(一定确保域名解析到这个机器的ip,关闭cf的云朵!),其他的参数最好也改一下

`docker-compose up -d  `

过一分钟等自动申请证书完毕后执行`docker container restart nginx`  (因为才入了个门docker,不太清楚怎么控制启动顺序,只能启动失败后重启一下了)

看看是不是可以了,客户端配置文件在`/root/config/client.json` 改个名本地用v2跑一下即可连上
记得手机客户端连接的话,手动设置时证书域名这个不要填,否则就算连上了速度也不超过10kb,原因未知

在vultr多个机器上测试通过.*三分钟*部署完成

机器重启后要重新开docker才行,进入目录 `docker-compose up -d  `然后`docker container restart nginx` 


