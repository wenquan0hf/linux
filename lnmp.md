# LNMP 环境搭建

<span>和</span><span>LAMP</span><span>不同的是</span><span>LNMP</span><span>中的</span><span>N</span><span>指的是是</span><span>Nginx</span><span>（类似于</span><span>Apache</span><span>的一种</span><span>web</span><span>服务软件）其他都一样</span><span>。</span><span>目前这种环境应用的也是非常之多</span><span>。Nginx</span><span>设计的初衷是提供一种快速高效多并发的</span><span>web</span><span>服务软件</span><span>。</span><span>在静态页面的处理上</span><span>Nginx</span><span>的确胜</span><span>Apache</span><span>一筹，然而在动态页面的处理上</span><span>Nginx</span><span>并不比</span><span>Apache</span><span>有多少优势</span><span>。</span><span>但是，目前还是有很多爱好者对</span><span>Nginx</span><span>比较热衷，随着</span><span>Nginx</span><span>的技术逐渐成熟，它在</span><span>web</span><span>服务软件领域的地位越来越高</span><span>。</span>

<span>【MySQL</span><span>安装</span><span>】</span>

<span>1\.</span> <span>下载</span><span>mysql</span><span>到</span><span>/usr/local/src/</span>

<span>cd /usr/local/src/</span>

<span>wget http://syslab.comsenz.com/downloads/linux/mysql-5.0.86-linux-i686-icc-glibc23.tar.gz</span>

<span>2\.</span> <span>解压</span>

<span>tar zxvf /usr/local/src/ mysql-5.0.86-linux-i686-icc-glibc23.tar.gz</span>

<span>3\.</span> <span>把解压完的</span><span>数据</span><span>移动到</span><span>/usr/local/mysql</span>

<span>mv mysql-5.0.86-linux-i686-ii-glibc23 /usr/local/mysql</span>

<span>4\.</span> <span>建立</span><span>mysql</span><span>用户</span>

<span>useradd mysql</span>

<span>5\.</span> <span>初始化数据库</span>

<span>cd /usr/local/mysql</span>

<span>mkdir /data/mysql ; chown -R mysql:mysql /data/mysql</span>

<span>./scripts/mysql_install_db --user=mysql --datadir=/data/mysql</span>

<span>--user</span><span>定义数据库的所属主，</span><span>--datadir</span><span>定义数据库安装到哪里，建议放到大空间的分区上，这个目录需要自行创建</span><span>。</span>

<span>6\.</span> <span>拷贝配置文件</span>

<span>cp support-files/my-large.cnf /etc/my.cnf</span>

<span>7\.</span> <span>拷贝启动脚本文件并修改其属性</span>

<span>cp support-files/mysql.server  /etc/init.d/mysqld</span>

<span>chmod 755 /etc/init.d/mysqld</span>

<span>8\.</span> <span>修改启动脚本</span>

<span>vim /etc/init.d/mysqld</span>

<span>需要修改的地方有</span><span>datadir=/data/mysql</span><span>（前面初始化数据库时定义的目录）</span>

<span>9\.</span> <span>把启动脚本加入系统服务项，并设定开机启动，启动</span><span>mysql</span>

<span>chkconfig --add mysqld</span>

<span>chkconfig mysqld on</span>

<span>service mysqld start</span>

<span>如果启动不了，请到</span><span>/data/mysql/</span> <span>下查看错误日志，该日志格式为主机名</span><span>.err。</span>

<span>【</span><span>**php**</span><span>**的安装**</span><span>】</span>

<span>这里要先声明一下，针对</span><span>Nginx</span><span>的</span><span>php</span><span>安装和针对</span><span>apache</span><span>的</span><span>php</span><span>安装是有区别的，因为</span><span>Nginx</span><span>中的</span><span>php</span><span>是以</span><span>fastcgi</span><span>的方式结合</span><span>nginx</span><span>的，可以理解为</span><span>nginx</span><span>代理了</span><span>php</span><span>的</span><span>fastcgi</span><span>，而</span><span>apache</span><span>是把</span><span>php</span><span>作为自己的模块来调用的</span><span>。</span>

<span>useradd www</span>

<span>cd /usr/local/src/</span>

<span>wget http://syslab.comsenz.com/downloads/linux/php-5.2.10.tar.gz</span>

<span>wget http://syslab.comsenz.com/downloads/linux/php-5.2.10-fpm-0.5.13.diff.gz</span>

<span>下载的第二个包</span><span>php-5.2.10-fpm-0.5.13.diff.gz</span><span>是用来给</span><span>php</span><span>打补丁的，默认情况下，</span><span>php</span><span>是无法编译出</span><span>fastcgi</span><span>的</span><span>。</span>

<span>tar zxvf php-5.2.10.tar.gz</span>

<span>gzip -cd php-5.2.10-fpm-0.5.13.diff.gz | patch -d php-5.2.10 -p1</span>

<span>cd php-5.2.10</span>

<span>./</span><span>conf</span><span>igure --prefix=/usr/local/php --with-config-file-path=/usr/local/php/etc --with-</span><span>mysql</span><span>=/usr/local/my</span><span>sql</span> <span>--with-mysql-sock=/tmp --with-libxml-dir --with-gd --with-jpeg-dir --with-png-dir --with-freetype-dir --with-iconv-dir --with-zlib-dir --with-mcrypt=/usr/local/libmcrypt --enable-soap --enable-gd-native-ttf --enable-ftp --enable-mbstring --enable-exif --enable-zend-multibyte --disable-ipv6 --enable-fastcgi --enable-fpm</span>

<span>make && make install</span>

<span>mkdir /usr/local/php/etc</span>

<span>cp php.ini-dist /usr/local/php/etc/php.ini  </span>

<span>vim /usr/local/php/etc/php-fpm.conf</span>

<span><value name="listen_address">/tmp/php-fcgi.sock</value></span> <span>这一行要改成这样，这里这样修改了以后，在配置</span><span>nginx</span><span>的时候就需要注意这个路径了</span><span>。
</span><span>修改</span><span>用户</span><span>和组的名称为</span><span>”www” 
</span><span>去掉注释，改成这样：</span><span>
Unix user of processes
                        <value name="user">www</value>
                        Unix group of processes
                        <value name="group">www</value></span>

<span>/usr/local/php/sbin/php-fpm start</span>

<span>其他关于</span><span>php</span><span>的扩展模块安装请参考：</span>

<span><a>CentOS 5.5下安装mysql5.1.57+php5.2.17(FastCGI)+nginx1.0.1高性能Web服务器</a>
</span>

<span>【</span><span>**nginx** </span><span>**安装以及配置**</span><span>】</span>

<span>**1\. nginx**</span><span>**源码安装**</span>

<span>cd /usr/local/src/</span>

<span>wget http://syslab.comsenz.com/downloads/linux/nginx-0.9.6.tar.gz</span>

<span>tar zxvf nginx-0.9.6.tar.gz</span>

<span>cd nginx-0.9.6</span>

<span>./configure --prefix=/usr/local/nginx --sbin-path=/usr/local/nginx/sbin/nginx --conf-path=/usr/local/nginx/conf/nginx.conf --error-log-path=/usr/local/nginx/logs/error.log --http-log-path=/usr/local/nginx/logs/access.log --pid-path=/usr/local/nginx/var/nginx.pid --lock-path=/usr/local/nginx/var/nginx.lock --http-client-body-temp-path=/dev/shm/nginx_temp/client_body --http-proxy-temp-path=/dev/shm/nginx_temp/proxy --http-fastcgi-temp-path=/dev/shm/nginx_temp/fastcgi --user=www --group=www --with-cpu-opt=pentium4F --without-select_module --without-poll_module --with-http_realip_module --with-http_sub_module --with-http_gzip_static_module --with-http_stub_status_module --without-http_ssi_module --without-http_userid_module --without-http_geo_module --without-http_memcached_module --without-http_map_module --without-mail_pop3_module --without-mail_imap_module --without-mail_smtp_module --with-pcre</span>

<span>make && make install</span>

<span>mkdir /dev/shm/nginx_temp</span>

<span>有的</span><span>nginx</span><span>版本编译时会因为</span><span>pcre</span><span>编译</span><span>不过去，需要修改一下</span> <span>--with-pcre=/usr/local/src/pcre-7.8</span><span>，前提是已经</span><span>下载</span><span>了</span><span>pcre</span><span>源码</span><span>包</span><span>pcre-7.8.tar.gz</span><span>，并解压到</span><span>/usr/local/src/pcre-7.8</span><span>，不需要编译</span><span>pcre</span>

<span>**2\.** </span><span>**编写**</span><span>**nginx**</span><span>**的启动脚本，并加入系统服务**</span>

<span>vi /etc/init.d/nginx</span> <span>写入以下内容：</span>

<span>#!/bin/bash
# chk</span><span>conf</span><span>ig: - 30 21
# description: http service.
# Source Function Library
. /etc/init.d/functions
#</span> <span>Nginx</span> <span>Settings
NGINX_SBIN="/usr/local/nginx/sbin/nginx"
NGINX_CONF="/usr/local/nginx/conf/nginx.conf"
NGINX_PID="/usr/local/nginx/var/nginx.pid"
RETVAL=0
prog="Nginx"
start() {
        </span><span>echo</span> <span>-n $"Starting $prog: "
        mkdir -p /dev/shm/nginx_temp
        daemon $NGINX_SBIN -c $NGINX_CONF
        RETVAL=$?
        echo
        return $RETVAL
}
stop() {
        echo -n $"Stopping $prog: "
        killproc -p $NGINX_PID $NGINX_SBIN -TERM
        rm -rf /dev/shm/nginx_temp
        RETVAL=$?
        echo
        return $RETVAL
}
reload(){
        echo -n $"Reloading $prog: "
        killproc -p $NGINX_PID $NGINX_SBIN -HUP
        RETVAL=$?
        echo
        return $RETVAL
}
restart(){
        stop
        start
}
config</span><span>test</span><span>(){
    $NGINX_SBIN -c $NGINX_CONF -t
    return 0
}
case "$1" in
  start)
        start
        ;;
  stop)
        stop
        ;;
  reload)
        reload
        ;;
  restart)
        restart
        ;;
  configtest)
        configtest
        ;;
  *)
        echo $"Usage: $0 "
        RETVAL=1
esac

exit $RETVAL</span>

<span>保存后，更改</span><span>/etc/init.d/nginx</span><span>的权限</span>

<span>chmod 755 /etc/init.d/nginx</span>

<span>chkconfig --add nginx</span>

<span>chkconfig nginx on</span>

<span>**3\. nginx**</span><span>**的配置**</span>

<span>vim /usr/local/nginx/conf/nginx.conf</span>

<span>把原来的文件清空，然后粘贴如下内容：</span>

<span>user www www;</span>

<span>worker_processes 2;</span>

<span>error_log /usr/local/nginx/logs/nginx_error.log crit;</span>

<span>pid /usr/local/nginx/var/nginx.pid;</span>

<span>#Specifies the value for maximum file descriptors that can be opened by this process.</span>

<span>worker_rlimit_nofile 51200;</span>

<span>events</span>

<span>{</span>

<span>use epoll;</span>

<span>worker_connections 6000;</span>

<span>}</span>

<span>http</span>

<span>{</span>

<span>include mime.types;</span>

<span>default_type application/octet-stream;</span>

<span>server_names_hash_bucket_size 2048;</span>

<span>server_names_hash_max_size 4096;</span>

<span>log_format combined_realip '$remote_addr $http_x_forwarded_for [$time_local] '</span>

<span>'$host "$request_uri" $status '</span>

<span>'"$http_referer" "$http_user_agent"';</span>

<span>sendfile on;</span>

<span>tcp_nopush on;</span>

<span>keepalive_timeout 30;</span>

<span>client_header_timeout 3m;</span>

<span>client_body_timeout 3m;</span>

<span>send_timeout 3m;</span>

<span>connection_pool_size 256;</span>

<span>client_header_buffer_size 1k;</span>

<span>large_client_header_buffers 8 4k;</span>

<span>request_pool_size 4k;</span>

<span>output_buffers 4 32k;</span>

<span>postpone_output 1460;</span>

<span>client_max_body_size 10m;</span>

<span>client_body_buffer_size 256k;</span>

<span>client_body_temp_path /usr/local/nginx/client_body_temp;</span>

<span>proxy_temp_path /usr/local/nginx/proxy_temp;</span>

<span>fastcgi_temp_path /usr/local/nginx/fastcgi_temp;</span>

<span>fastcgi_intercept_errors on;</span>

<span>tcp_nodelay on;</span>

<span>gzip on;</span>

<span>gzip_min_length 1k;</span>

<span>gzip_buffers 4 8k;</span>

<span>gzip_comp_level 5;</span>

<span>gzip_http_version 1.1;</span>

<span>gzip_types text/plain application/x-javascript text/css text/htm application/xml;</span>

<span>server</span>

<span>{</span>

<span>listen 80;</span>

<span>server_name www.example.com;</span>

<span>index index.html index.htm index.php;</span>

<span>root /data/www;</span>

<span>location ~ \.php$ {</span>

<span>include fastcgi_params;</span>

<span>fastcgi_pass unix:/ php-fcgi.sock;</span>

<span>fastcgi_index index.php;</span>

<span>fastcgi_param SCRIPT_FILENAME /data/www$fastcgi_script_name;</span>

<span>}</span>

<span>}</span>

<span>保存后就可以启动</span><span>nginx</span><span>了，在重启之前最好先检查一下是否有问题
</span><span>
/usr/local/nginx/sbin/nginx  -t   如果显示 "syntax is ok  和  nginx.conf was tested successfully"这样的信息，就说明配置没有问题了，否则就需要根据提示修改了。
service nginx start</span>

<span>如果启动不了，请到</span><span>/usr/local/nginx/logs/</span><span>目录下查看<font>nginx_</font></span><span><font>error.log</font></span><span>这个日志文件</span><span>。若是没有这个日志文件，很有可能是那个目录没有写权限，请执行

chmod +w /usr/local/nginx/logs/ 
service  nginx  restart</span>

【测试是否解析php文件】

 vim /data/www/1.php 

写入如下内容： 然后设定hosts文件，

访问 www.92csz.com/1.php 看是否能解析出这个页面。