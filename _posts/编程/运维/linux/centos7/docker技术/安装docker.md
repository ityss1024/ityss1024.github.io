

```shell
#! /bin/bash
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
sudo yum-config-manager \
    --add-repo \
    https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/centos/docker-ce.repo

sudo yum install docker-ce docker-ce-cli containerd.io -y

sudo systemctl start docker
sudo systemctl enable docker
# 切换国内镜像
sudo touch  /etc/docker/daemon.json
# 写入内容
sudo cat>/etc/docker/daemon.json <<END
{"registry-mirrors":["https://docker.mirrors.ustc.edu.cn/"]}
END

# 安装docker-compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
docker-compose --version && docker --version && docker info
```

