# elk_docker-compose


1、克隆项目

git clone https://github.com/zuiye/elk_docker-compose.git

2、设置宿主机内核参数


echo vm.max_map_count=655360 >> /etc/sysctl.conf

sysctl -p


3、设置认证密码，需要先启动elasticsearch

cd elk_docker-compose

docker-compose up -d elasticsearch

然后设置认证密码

docker exec -ti elasticsearch /usr/share/elasticsearch/bin/elasticsearch-setup-passwords interactive

记住设置的密码，建议全部设置一样, 会连续设置好几个的密码，会提示输入密码，输入完就设置好了密码，接着就需要修改配置文件的密码和elasticsearch IP


4、修改kibana和logstash配置里的密码

修改kibana配置中的密码，密码为刚才设置的密码

sed -i "s/123456/yourpassword/g" /opt/elk_docker-compose/kibana/config/kibana.yml


修改logstash配置中的密码，密码为刚才设置的密码

sed -i "s/123456/yourpassword/g" /opt/elk_docker-compose/logstash/config/logstash.conf


sed -i "s/123456/yourpassword/g" /opt/elk_docker-compose/logstash/config/logstash.yml


5、启动所有容器

docker-compose up -d
