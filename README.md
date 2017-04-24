# opsSAM
# 后续视情况开源，有定制化需求可单独联系

目前已实现的功能：
1、dashboard控制台；
2、自动化装机系统；
3、服务器、网络设备、IDC资产管理；
4、基于SSH的远程批量命令，文件分发；
5、基于Salt的的远程批量命令；
6、基于Salt的模块化部署，服务器初始化；
7、基于SVN的PHP、py代码发布系统；
8、定时任务调度系统(代码已完成，页面未实现)；
9、远程SSH终端连接主机和远程录像回放；
10、用户和栏目权限控制系统；
11、所有操作审计功能。

待实现：
1、KVM管理集成到自动化装机系统；
2、docker容器化管理平台；
3、基于jenkins的java代码发布。


一、基本环境

  os：    Centos 6.6 x86_64
  
  python: 2.6.6 


二、依赖关系

  1、python依赖包
  
    pip install -r requirements.txt

  2、epel源rpm安装包
  
    mysql-5.5.19
    
    subversion-1.6.11-10
    
    rabbitmq-server-3.1.5-1
    
    cobbler-2.6.3-1
    

  3、其他接口
  
    a)cobbler服务器
      cobbler-2.6.3-1.el6.noarch
      cobbler-web-2.6.3-1.el6.noarch
      
    b)saltstack服务器
      salt 2014.7.2 
      salt-api-2014.7.2

    c)svn服务器
      subversion-1.6.11-11

  4、启动数据库
  
    a)创建登陆用户
      /etc/init.d/mysqld start
      mysqladmin -uroot password opsSAM

    b)创建数据库：
      mysql -uroot -popsSAM -e "create database opsSAM;"

    c)生成项目数据表：
      cd /your/sitepath/
      python manage.py syncdb

    d)创建初始登陆用户admin(密码admin)：
      mysql -uroot -popsSAM -e "insert into opsSAM.opsSAM_users(username,password,admin) values ('admin','f313176847fcc0c82dae8e51e0e40b1d33ec7f0fabf279c164f8541ec99f8a06f473b3b1439a41a898aa2f70f076a59bb671e17bed52471cb9adfee9701a7fb5','是');"

  5、设置django
  
    opsSAM.opsSAM.settings.py
    opsSAM.opsSAM.settings_local.py
  


三、django生产环境安装(非必须)

  推荐nginx+uwsgi(略)
  
  安装后按照实际情况修改scripts/supervisord.conf相关django配置
  
  [program:django]
  
  command=/usr/bin/python /your/sitepath/opsSAM/manage.py runserver 0.0.0.0:80


四、启动

  cp scripts/supervisord.conf /etc/
  
  cp scripts/supervisord /etc/init.d/
  
  chmod 755 /etc/init.d/supervisord
  
  /etc/init.d/supervisord start


五、访问地址：

  opsSAM前台：    http://your_ip/
  
  opsSAM后台：    http://your_ip/admin
  
  rabbitmq：      http://your_ip:15672/
  
  celery flower： http://your_ip:5555/
  
  supervisor:     http://your_ip:9001/
  

六、demo

![demo](https://github.com/MorningSong/opsSAM/blob/master/demo/login.png)

![demo](https://github.com/MorningSong/opsSAM/blob/master/demo/index.jpg)

![demo](https://github.com/MorningSong/opsSAM/blob/master/demo/system_install.png)

![demo](https://github.com/MorningSong/opsSAM/blob/master/demo/exec_command.png)

![demo](https://github.com/MorningSong/opsSAM/blob/master/demo/deploy_app.png)

![demo](https://github.com/MorningSong/opsSAM/blob/master/demo/deploy_code.png)

![demo](https://github.com/MorningSong/opsSAM/blob/master/demo/webssh.png)

联系QQ: 370049527

上海Linux运维技术QQ总群:253534961

二维码加入：

![demo](https://github.com/MorningSong/opsSAM/blob/master/demo/qq.png)
