# example

## Jira Mysql Setting
```
mysql -uroot -p
### If want to separation access account ###
mysql> create database jira default character set utf8 collate utf8_bin;
mysql> grant all on jira.* to 'jira'@'%' identified by 'password';
```

## Confluence Mysql Setting
```
CREATE DATABASE <database-name> CHARACTER SET utf8 COLLATE utf8_bin;
GRANT ALL PRIVILEGES ON <database-name>.* TO '<confluenceuser>'@'%' IDENTIFIED BY '<password>';
```

## JIRA Setup Database SSL Warring Config to false
```
vim /$pwd/JIRA_HOME_data/dbconfig.xml
```
```
[root@jt-jira jira]# cat /var/lib/docker/volumes/jira_JIRA_HOME_data/_data/dbconfig.xml 
...
    <url>jdbc:mysql://address=(protocol=tcp)(host=$IP)(port=3306)/jira?sessionVariables=default_storage_engine=InnoDB&amp;useSSL=false</url>
...
```
右边的</url>改为&amp;useSSL=false</url>
由于使用docker volume,可以直接宿主机上修改文件然后重启容器

## Confluence Setup Database SSL Warring Config to false
```
/$pwd/CONF_HOME_data/confluence.cfg.xml
jdbc:mysql://$IP:3306/confluence改为jdbc:mysql://$IP:3306/confluence?useSSL=false
```
改完后重启下容器即可
