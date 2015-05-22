# 配置 squid 服务

<span>【**什么是**</span>**<span><font>squid</font></span>**<span>】</span>

<span><font>Squid</font></span><span>是比较知名的代理软件，它不仅可以跑在</span><span><font>linux</font></span><span>上还可以跑在</span><span><font>windows</font></span><span>以及</span><span><font>Unix</font></span><span>上，它的技术已经非常成熟。目前使用</span><span><font>Squid</font></span><span>的用户也是十分广泛的。</span><span><font>Squid</font></span><span>与</span><span><font>Linux</font></span><span>下其它的代理软件如</span><span><font>Apache</font></span><span>、</span><span><font>Socks</font></span><span>、</span><span><font>TIS FWTK</font></span><span>和</span><span><font>delegate</font></span><span>相比，下载安装简单，配置简单灵活，支持缓存和多种协议。</span><span></span>

<span><font>Squid</font></span><span>的缓存功能相当好用，不仅可以减少带宽的占用，同样也大大降低了后台的</span><span><font>WEB</font></span><span>服务器的磁盘</span><span><font>I/O</font></span><span>的压力。</span><span><font>Squid</font></span><span>接收用户的下载申请，并自动处理所下载的数据。也就是说，当一个用户象要下载一个主页时，它向</span><span><font>Squid</font></span><span>发出一个申请，要</span><span><font>Squid</font></span><span>替它下载，然后</span><span><font>Squid</font> </span><span>连接所申请网站并请求该主页，接着把该主页传给用户同时保留一个备份，当别的用户申请同样的页面时，</span><span><font>Squid</font></span><span>把保存的备份立即传给用户，使用户觉得速度相当快。</span><span><font><span></span></font></span>

<span><font>Squid</font></span><span>将数据元缓存在内存中，同时也缓存</span><span><font>DNS</font></span><span>查寻的结果，除此之外，它还支持非模块化的</span><span><font>DNS</font></span><span>查询，对失败的请求进行消极缓存。</span><span><font>Squid</font></span><span>支持</span><span><font>SSL</font></span><span>，支持访问控制。由于使用了</span><span><font>ICP</font></span><span>，</span><span><font>Squid</font></span><span>能够实现重叠的代理阵列，从而最大限度的节约带宽。</span><span><font><span></span></font></span>

<span><font>Squid</font></span><span>对硬件的要求是内存一定要大，不应小于</span><span><font>128M</font></span><span>，硬盘转速越快越好，最好使用服务器专用</span><span><font>SCSI</font> </span><span>硬盘，处理器要求不高，</span><span><font>400MH</font></span><span>以上既可。</span>

<span>【**安装**</span>**<span><font>squid</font></span>**<span>】</span>

<span><font>wget http://www.squid-cache.org/Versions/v2/2.6/squid-2.6.STABLE20.tar.gz</font></span>

<span><font>tar zxvf squid-2.6.STABLE20.tar.gz</font></span>

<span><font>cd squid-2.6.STABLE20
ulimit -HSn 65535</font></span>

<span><font>useradd<span> </span> squid
</font></span><span><span><span>编译</span><span>参数</span></span></span><span>
<font>./<span><span>conf</span></span>igure --prefix=/usr/local/squid \
--disable-dependency-tracking \
--enable-dlmalloc \
--enable-gnuregex \
--disable-carp \
--enable-async-io=240 \
--with-pthreads \
--enable-storeio=ufs,aufs,diskd,null \
--disable-wccp \
--disable-wccpv2 \
--enable-kill-parent-hack \
--enable-cachemgr-hostname=localhost \
--enable-default-err-language=Simplify_Chinese \
--with-build-environment=POSIX_V6_ILP32_OFFBIG \
--with-maxfd=65535 \
--with-aio \
--disable-poll \
--enable-epoll \
--enable-linux-netfilter \
--enable-large-cache-files \
--disable-ident-lookups \
--enable-default-hostsfile=/etc/hosts \
--with-dl \
--with-large-files \
--enable-removal-policies=heap,lru \
--enable-delay-pools \
--enable-snmp \
--disable-internal-dns

make && make <span><span>install</span></span></font></span>

<span><span>关于</span></span><span><span><font>squid</font></span></span><span><span>的版本，有必要提一下，目前</span></span><span><span><font>squid</font></span></span><span><span>最新版本已经到了</span></span><span><span><font>3.1</font></span></span><span><span>了，但是笔者认为</span></span><span><span><font>2.6</font></span></span><span><span>版本比较好用，如果你有兴趣可以研究一下</span></span><span><span><font>3.1</font></span></span><span><span>。</span></span>

<span><span>【</span></span><span>**<span><font>squid</font></span>**</span><span>**<span>配置</span>**</span><span><span>】</span></span>

<span>编辑配置文件</span><span> <font>/usr/local/squid/etc/squid.conf</font></span>

<span>把原来配置文件删除，替换成：</span>

<span><font>http_port 80 transparent

cache_replacement_policy lru<span> </span> #</font></span><span>如果有多个（下面两行）缓存目录，则需要写这个参数</span><span>
<font>cache_dir aufs <span> </span>/cache1 8192 16 256<span> </span> #</font></span><span>缓存目录</span><span><font>1 /cache1</font> </span><span>大小为</span><span><font>8G
cache_dir aufs /cache2 4096 16 256<span> </span> #</font></span><span>缓存目录</span><span><font>2 /cache2</font> </span><span>大小为</span><span><font>4G</font></span>

<span><font>##</font> </span><span>上面两行定义了缓存目录，这个缓存目录可以只有一个，也可以定义很多个。</span><span>
<font>cache_mem 2048 MB<span> </span> #</font></span><span>分配多少内存给</span><span><font>squid</font></span><span>，建议留至少</span><span><font>512M</font></span><span>给系统，如果你是虚拟机内存很小，只作为试验用的话，那就分一半内存给</span><span><font>squid
maximum_object_size 2048 KB<span> </span> #</font></span><span>缓存的文件最大不能超过</span><span><font>2M
maximum_object_size_in_memory 512 KB #</font></span><span>缓存在内存中的文件最大不超过</span><span><font>512k
visible_hostname cache.example.com <span> </span>#</font></span><span>显示给用户的主机名</span><span><span>
<font>client_persistent_connections off<span> </span> #client</font></span></span><span>端关闭长连接</span><span>
<font>server_persistent_connections on<span> </span> #server</font></span><span>端打开长连接</span><span>
<font>memory_pools on
memory_pools_limit 1024 MB
forwarded_for on
log_icp_queries off
cache_mgr <span> </span><span>cache@example.com</span><span> </span> #</font></span><span>定义管理员的</span><span><font>mail</font></span><span>为</span><span><font>cache@example.com
via on
httpd_suppress_version_string off
cache_effective_user squid<span>  </span> #</font></span><span>定义以</span><span><font>squid</font></span><span>用户的身份运行</span><span><font>squid
cache_effective_group squid
error_directory /usr/local/squid/share/errors/Simplify_Chinese
icon_directory /usr/local/squid/share/icons
mime_table /usr/local/squid/etc/mime.<span><span>conf</span></span>
ie_refresh off
tcp_recv_bufsize 32 KB

acl all src 0.0.0.0/0.0.0.0
acl localhost src 127.0.0.0/8 
acl Mgr_ip src 127.0.0.0/8 
acl allow_ip dst 127.0.0.0/8  192.168.0.0/16<span> </span> #</font></span><span>定义允许代理的</span><span><font>web</font></span><span>的</span><span><font>IP</font></span><span>或者</span><span><font>IP</font></span><span>段</span><span>
<font>acl PURGE method PURGE
acl Safe_ports port 80 8080
acl CONNECT method CONNECT
acl manager proto cache_object
acl HTTP proto HTTP

http_access allow allow_ip
http_access allow manager Mgr_ip
http_access deny manager
http_access deny PURGE
http_access deny !Safe_ports
http_access deny all
icp_access deny all
ipcache_size 1024
ipcache_low 90
ipcache_high 95
memory_replacement_policy lru
hosts_file /etc/hosts
request_header_max_size 128 KB
hierarchy_stoplist cgi-bin ? \.php \.html
acl QUERY urlpath_regex cgi-bin \? \.php \.html
cache deny QUERY
quick_abort_min -1 KB
quick_abort_max 32 KB
quick_abort_pct 95
# error page
#error_map</font> <a><span><font>http://www.92csz.com/404.html</font></span></a> <font>403
#deny_info</font> <a><span><font>http://www.92csz.com/error.html</font></span></a> <font>cctv_Domain
# timeout
peer_connect_timeout 20 seconds
connect_timeout 20 seconds
read_timeout 60 seconds
request_timeout 20 seconds
pconn_timeout 20 seconds
shutdown_lifetime 5 seconds
strip_query_terms off
icp_port 0
# logfile
emulate_httpd_log on
logformat combined %>a %ui %un [%tl] "%rm %ru HTTP/%rv" %Hs %<st "%>h" "%>h" %Ss:%Sh
#access_log /log/squid-log/access.log combined
cache_store_log /dev/null
cache_log /var/log/squid/cache.log
logfile_rotate 12
# MISCELLANEOUS
store_objects_per_bucket 15
client_db off</font></span>

<span>修改完配置文件后保存，然后初始化</span><span><font>squid</font></span>

**<span><font>mkdir /cache1<span> </span> /cache2 /var/log/squid</font></span>**

**<span><font>chown -R squid:squid /cache1 /cache2 /var/log/squid</font></span>**

<font>**<span>/usr/local/squid/sbin/squid</span> **<span><span> </span>**-z** <span> </span></span></font>

<span><font>#</font> </span><span>用来生成</span><span><font>cache</font></span><span>目录，如果你的配置文件配置出错，往往会在初始化的时候报错，错误信息会直接显示在屏幕上。初始化成功后，就可以启动</span><span><font>squid</font></span><span>了，启动命令为：</span><span></span>

**<span><font>nohup /usr/local/squid/bin/RunCache &</font></span>**

<span>启动后，可以去看看</span><span><font>cache.log</font> </span><span>在这个日志中，你可以看到很多关于</span><span><font>squid</font></span><span>的信息，当然也包括一些错误日志。</span><span></span>

<span>如果想开机启动则需要在</span><span><font>/etc/rc.d/rc.local</font></span><span>中最后加入一行</span><span></span>

<span><font>/usr/local/bin/RunCache &</font></span>

<span>到这里算是配置完成了，但是还有一个问题，就是如何定义被代理的</span><span><font>web</font></span><span>以及域名？单单看配置文件并没有说代理的</span><span><font>web</font></span><span>是哪一个。确实，这个配置文件其实可以代理多台</span><span><font>web</font></span><span>，只要你在</span><span><font>/etc/hosts</font></span><span>中定义要代理的域名以及</span><span><font>IP</font></span><span>即可，</span><span><font>hosts</font></span><span>格式在前面已经介绍过。笔者要提醒你的是，<span>如果是一台</span></span><span><font>web</font></span><span>上的多个域名，请不要写一行，虽然</span><span><font>hosts</font></span><span>是允许的，但是如果写成一个</span><span><font>IP</font></span><span>对应多个域名，</span><span><font>squid</font></span><span>代理时就会出错。所以有几个域名就要写几行。</span>

<span>更改</span><span><font>/etc/hosts</font></span><span>后要重启</span><span><font>squid</font></span><span>才能生效：</span><span></span>

**<span><font>/usr/local/squid/sbin/squid<span> </span> -krec</font></span>**

<span>在重启前可以先检测一下，是否有错，命令为：</span><span></span>

**<span><font>/usr/local/squid/sbin/squid –kcheck</font></span>**

<span>如果没有错，则不会显示任何信息，否则会显示一些信息出来。</span>

