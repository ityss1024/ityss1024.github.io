

参考 https://www.cnblogs.com/dbf-/p/11031736.html

```shell
#! /bin/bash
sudo yum update -y
sudo yum makecache
sudo yum -y groupinstall "Development tools"
sudo yum install openssl-devel bzip2-devel expat-devel gdbm-devel readline-devel sqlite-devel -y
# 下载官网 https://www.anaconda.com/distribution/
wget https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh
# bash Anaconda3-2019.03-Linux-x86_64.sh -y
# 参考 https://www.cnblogs.com/dbf-/p/11031736.html
```

