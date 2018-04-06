1.安装svn软件：
	yum -y install subversion
	(-y 自动)

2.安装apr，apr-util插件
    	下载网址：http://apr.apache.org/download.cgi
    	其实就是如下网址：

    	apr插件：http://mirrors.noc.im/apache//apr/apr-1.5.2.tar.gz
    	apr-util插件：http://mirrors.noc.im/apache//apr/apr-util-1.5.4.tar.gz	 
    
    	wget 粘贴链接地址
    	（回车下载，complet完成，两个插件）

3.解压缩文件：
	tar -zxvf 文件名
	（回车解压，两个文件，ls查看解压文件）

4.编译安装：
	cd apr-1.5.2
	(进入目录)
	./configure —-prefix=/usr/local/apr
	(回车将文件安装到／usr／local／apr)
	cd ..
	（回到上级目录）
	 cd apr-util-1.5.4
	(进入)	
	./configure  —-prefix=/usr/local/apr-util —-with-apr=/usr/local/apr
	(回车编译)
	make
	（再次编译）
	make install
	（安装）
5.配置：
	vi /etc/ld.so.conf
	(回车 i)
	／usr/local/apr/lib
	/usr/local/apr-util/lib
	(保存退出)
	ldconfigure -v
	(加载配置)

6.创建仓库：
	cd ／
	mkdir /wangluo
	(随意目录)	
	cd /wangluo
	mkdir svn
	mkdir ./svn/project1
	mkdir ./svn/project2
	svnadmin create /wangluo/svn/project1
	svnadmin create /wangluo/svn/project2
	(创建成功)
7.svn配置文件
	cd /wangluo/svn/project1
	ls
	cd conf
	ls
	vi svnserve.conf
	(进入文件，去掉anon-acces=read和下面三个文件前面的#去掉)	
	vi passed
	（在[users] 之下，添加用户名 = 密码
	project1 = project1
	project2 = project2）
	
	vi authz
	(在这个文件中在[groups]之下，admin = 用户名
	project1 = project1
	project2 = project2
	后两个是组 = 用户名

	[/]
	@admin = rw
	
	[project1:/]
	@admin = rw
	@project1 = tw
	:wq
	
	)		
	cd ..
	ls
	cd .. 
	ls
	(到svn根目录下)
	cp -r ./project1/conf ./
	(复制后回车)
	
8.防火墙配置：
	vi ／etc/sysconfig/iptables
	(svn 默认端口号3690，复制一个端口，server一行改为3690)
	service iptables restart
	(重启防火墙)

9.启动svn服务器：
	svnserve -d -r /wangluo/svn/
10.客户端链接：
	（其余未完网址：http://v.youku.com/v_show/id_XMTUyMjYwNDc0OA==.html?isPurchase=0&categoryId=12&albumId=0&tvId=0&vId=&sourceCode=&sourceName=&source=embedplay&platform=&albumName=svn%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%90%AD%E5%BB%BA-linux%E7%B3%BB%E7%BB%9F(centos)&uploaderId=&isExclusive=false&siteName=%E4%BC%98%E9%85%B7&siteId=youku&itemTitle=svn%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%90%AD%E5%BB%BA-linux%E7%B3%BB%E7%BB%9F(centos)&itemPlayerLink=&sourceUrl=http%3A%2F%2Fv.youku.com%2Fv_show%2Fid_XMTUyMjYwNDc0OA%3D%3D.html）		
