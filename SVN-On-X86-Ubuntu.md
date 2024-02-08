$ sudo apt-get update  
$ sudo apt-get install subversion  
$ mkdir -p ~/svn/repository  
$ chmod -R 777 ~/svn/repository  
$ svnadmin create ~/svn/repository   

$ mv ~/svn/repository/conf/svnserve.conf ~/svn/repository/conf/svnserve.conf.bak  
$ cp ~/svn/repository/conf/svnserve.conf.bak ~/svn/repository/conf/svnserve.conf  
$ vim ~/svn/repository/conf/svnserve.conf  

anon-access = none  
auth-access = write  
password-db = passwd  
authz-db = authz  

$ mv ~/svn/repository/conf/authz ~/svn/repository/conf/authz.bak  
$ cp ~/svn/repository/conf/authz.bak ~/svn/repository/conf/authz  
$ vim ~/svn/repository/conf/authz  

admin = zkw  
[repository:/]  
@admin = rw  
* =  

$ mv ~/svn/repository/conf/passwd ~/svn/repository/conf/passwd.bak  
$ cp ~/svn/repository/conf/passwd.bak ~/svn/repository/conf/passwd  
$ vim ~/svn/repository/conf/passwd  

zkw = ZKW123  

$ svnserve -d -r ~/svn  
$ ps -aux|grep svnserve  
$ killall svnserve  

$ sudo touch /etc/systemd/system/svn.service  
$ sudo chmod 664 /etc/systemd/system/svn.service  
$ sudo vim /etc/systemd/system/svn.service  

[Unit]  
Description=Subversion Server  
[Service]  
Type=forking  
ExecStart=/usr/bin/svnserve -d -r /home/zkw/svn  
ExecStop=/usr/bin/killall svnserve  
Restart=always  
[Install]  
WantedBy=default.target  

$ systemctl daemon-reload  

$ systemctl start svn.service  
$ systemctl stop svn.service  

$ systemctl enable svn.service  

[Ref:](https://zhuanlan.zhihu.com/p/377181219)  
