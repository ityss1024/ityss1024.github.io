

```shell
#!/bin/bash
sudo yum install ntpdate -y && ntpdate -u ntp.aliyun.com
sudo mv /etc/localtime{,.bak} && sudo ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
sudo sed -i "s/SELINUX=enforcing/SELINUX=disabled/" /etc/selinux/config && sudo setenforce 0
sudo rpm -ivh http://repo.zabbix.com/zabbix/5.4/rhel/7/x86_64/zabbix-release-5.4-1.el7.noarch.rpm && sudo yum -y install zabbix-agent2 zabbix-sender
sudo yum -y install zabbix-agent2 zabbix-sender
sudo firewall-cmd --zone=public --add-port=10050/tcp --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --zone=public --list-ports
## 修改配置文件 第一个参数是ip地址 第二个参数是主机名称
sudo sed -i "s/127.0.0.1/$1/g"  /etc/zabbix/zabbix_agent2.conf
sudo sed -i "s/Zabbix server/$2/g" /etc/zabbix/zabbix_agent2.conf
sudo systemctl start zabbix-agent2.service
sudo systemctl enable zabbix-agent2.service
sudo yum install telnet -y  
sudo telnet "$1" 10051
sudo tailf /var/log/zabbix/zabbix_agent2.log
sudo ps aux|grep zabbix
```

