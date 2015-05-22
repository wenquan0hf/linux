# 配置 FTP 服务 

<font><span>【**什么是**</span>**<span><font>FTP</font></span>**<span>】</span></font>

<font><span>也许你对</span><span><font>FTP</font></span><span>不陌生，但是你是否了解</span><span><font>FTP</font></span><span>到底是个什么玩意？</span><span><font>FTP</font> </span><span>是</span><span><font>File Transfer Protocol</font></span><span>（文件传输协议）的英文简称，而中文简称为“文传协议”。用于</span><span><font>Internet</font></span><span>上的控制文件的双向传输。同时，它也是一个应用程序（</span><span><font>Application</font></span><span>）。用户可以通过它把自己的</span><span><font>PC</font></span><span>机与世界各地所有运行</span><span><font>FTP</font></span><span>协议的服务器相连，访问服务器上的大量程序和信息。</span><span><font>FTP</font></span><span>的主要作用，就是让用户连接上一个远程计算机（这些计算机上运行着</span><span><font>FTP</font></span><span>服务器程序）察看远程计算机有哪些文件，然后把文件从远程计算机上拷到本地计算机，或把本地计算机的文件送到远程计算机去。</span><span><font>FTP</font></span><span>用的比</span><span><font>NFS</font></span><span>更多，所以你一定要熟练配置它。</span></font>

<font><span>【**配置**</span>**<span><font>ftp</font></span>**<span>】</span></font>

<font><span>安装</span><span><font>Redhat/CentOS</font></span><span>系统时也许你会连带着把</span><span><font>ftp</font></span><span>装上，系统默认带的</span><span><font>ftp</font></span><span>是</span><span><font>vsftp</font></span><span>，比较常用，配置也很简单。但笔者常使用的</span><span><font>ftp</font></span><span>软件为</span><span><font>pure-ftpd</font></span><span>。因为这个软件比</span><span><font>vsftp</font></span><span>配置起来更加灵活和安全。下面是笔者配置</span><span><font>pure-ftpd</font></span><span>的过程：</span>

</font>

<font><span>下载最新的</span><span><font>pure-ftp</font></span><span>源码包</span><span><font>pure-ftpd-1.0.21.tar.bz2<span>  </span></font></span></font>

<span># wget http://syslab.comsenz.com/downloads/linux/pure-ftpd-1.0.21.tar.bz2</span>

<span>#tar jxvf pure-ftpd-1.0.21.tar.bz2</span>

<span>#cd pure-ftpd-1.0.21</span>

<span>./configure \</span>

<span>"--prefix=/usr/local/pureftpd" \</span>

<span>"--without-inetd" \</span>

<span>"--with-altlog" \</span>

<span>"--with-puredb" \</span>

<span>"--with-throttling" \</span>

<span>"--with-largefile" \</span>

<span>"--with-peruserlimits" \</span>

<span>"--with-tls" \</span>

<span>"--with-language=simplified-chinese"</span>

<span>#make && make install</span>

<font><span>启动</span></font>

<font><span>用配置文件</span></font>

<span>#mkdir /usr/local/pureftpd/etc</span>

<span>#cd configuration-file</span>

<span>#cp pure-ftpd.conf /usr/local/pureftpd/etc/pure-ftpd.conf</span>

<span>#cp pure-config.pl<span> </span> /usr/local/pureftpd/sbin/pure-config.pl</span>

<span>#chmod 755 /usr/local/pureftpd/sbin/pure-config.pl</span>

<font><span>在启动pure-ftp之前需要先修改配置文件，配置文件为/usr/local/pureftpd/etc/pure-ftpd.conf,你可以打开看一下，里面内容很多，如果你英文好，可以好好研究一番，下面是我的配置文件，如果你嫌麻烦，直接拷贝过去即可。</span></font>

<span>____________________________________</span>

<span>ChrootEveryone<span>             </span> yes</span>

<span>BrokenClientsCompatibility<span> </span> no</span>

<span>MaxClientsNumber<span>           </span> 50</span>

<span>Daemonize<span>                  </span> yes</span>

<span>MaxClientsPerIP<span>            </span> 8</span>

<span>VerboseLog<span>                 </span> no</span>

<span>DisplayDotFiles<span>            </span> yes</span>

<span>AnonymousOnly<span>              </span> no</span>

<span>NoAnonymous<span>                </span> no</span>

<span>SyslogFacility<span>             </span> ftp</span>

<span>DontResolve<span>                </span> yes</span>

<span>MaxIdleTime<span>                </span> 15</span>

<span>PureDB<span>                       </span> /usr/local/pureftpd/etc/pureftpd.pdb</span>

<span>LimitRecursion<span>             </span> 2000 8</span>

<span>AnonymousCanCreateDirs<span>     </span> no</span>

<span>MaxLoad<span>                    </span> 4</span>

<span>AntiWarez<span>                  </span> yes</span>

<span>Umask<span>                      </span> 133:022</span>

<span>MinUID<span>                     </span> 100</span>

<span>AllowUserFXP<span>               </span> no</span>

<span>AllowAnonymousFXP<span>          </span> no</span>

<span>ProhibitDotFilesWrite<span>      </span> no</span>

<span>ProhibitDotFilesRead<span>       </span> no</span>

<span>AutoRename<span>                 </span> no</span>

<span>AnonymousCantUpload<span>        </span> no</span>

<span>PIDFile<span>                    </span> /usr/local/pureftpd/var/run/pure-ftpd.pid</span>

<span>MaxDiskUsage<span>              </span> 99</span>

<span>CustomerProof<span>             </span> yes</span>

<font><span><font>####################################到此结束，保存即可#########################</font></span></font>

<font><span>启动命令：</span><span> <font>/usr/local/pureftpd/sbin/pure-config.pl /usr/local/pureftpd/etc/pure-ftpd.conf</font></span></font>

<font><span><font>#######</font></span><span>接下来该建立用户了</span><span><font>###############</font></span></font>

<font><span><font># /usr/local/pureftpd/bin/pure-pw useradd ftp_test -u www -d /data/wwwroot</font></span><span>其中，</span><span><font>-u</font> </span><span>将虚拟用户</span><span> <font>ftp_test</font> </span><span>与系统用户</span><span> <font>www</font> </span><span>关联在一起。</span><span><font>-d</font> </span><span>参数使</span><span> <font>ftp_test</font> </span><span>只能访问其主目录。执行完上述命令后，会提示输入密码。</span></font>

<font><span># /usr/local/pureftpd/bin/pure-pw mkdb</span></font>


