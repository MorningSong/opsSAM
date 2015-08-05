# opsSAM

一、基本环

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
  opsSAM前台：    http://192.168.3.105/
  opsSAM后台：    http://192.168.3.105/admin
  rabbitmq：      http://192.168.3.105:15672/
  celery flower： http://192.168.3.105:5555/
  supervisor:     http://192.168.3.105:9001/
