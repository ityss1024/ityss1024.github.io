

参考 https://www.javatt.com/p/53521

```javascript
// 从清华源下载 jdk 下载很快  大概5-6m/s
wget https://mirrors.tuna.tsinghua.edu.cn/AdoptOpenJDK/8/jdk/x64/linux/OpenJDK8U-jdk_x64_linux_openj9_8u292b10_openj9-0.26.0.tar.gz
```



```shell
sudo vim /etc/profile
```

追加一下内容  变量值根据你自身jdk路径来定

```shell
JAVA_HOME=/home/soft_ware/jdk/jdk1.7.0_79
JRE_HOME=$JAVA_HOME/jre 
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin     
CLASSPATH=:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
export JAVA_HOME JRE_HOME PATH CLASSPATH
```

```shell
source /etc/profile
```

