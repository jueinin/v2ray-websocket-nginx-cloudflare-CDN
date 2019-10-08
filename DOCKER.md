### 安装与使用
首先安装docker和docker-compose
- 安装docker
    - curl -fsSL https://get.docker.com -o get-docker.sh
    - sh get-docker.sh
- 安装docker-compose
    - curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    - chmod +x /usr/local/bin/docker-compose
- 安装git
    - apt install git -y
`git clone git@github.com:jueinin/v2ray-websocket-nginx-cloudflare-CDN.git`
`cd v2`  然后编辑Dockerfile-main,修改$V2RAY_DOMAIN为你的域名(一定确保),其他的参数最好也改一下

`docker-compose up -d  `

`docker container restart nginx`

看看是不是可以了,客户端配置文件在`/root/config/client.json` 改个名本地用v2跑一下即可连上
