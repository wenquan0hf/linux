# NFS 服务配置

<font><span>【**什么是**</span>**<span><font>NFS</font></span>**<span>】</span><span><font><span>    </span></font></span></font>

<font><span><font>NFS</font></span><span>会经常用到，用于在网络上共享存储。这样讲，你对</span><span><font>NFS</font></span><span>可能不太了解，笔者不妨举一个例子来说明一下</span><span><font>NFS</font></span><span>是用来做什么的。假如有三台机器</span><span><font>A</font></span><span>、</span><span><font>B</font></span><span>、</span><span><font>C</font></span><span>，它们需要访问同一个目录，目录中都是图片，传统的做法是把这些图片分别放到</span><span><font>A</font></span><span>、</span><span><font>B</font></span><span>、</span><span><font>C</font></span><span>。但是使用</span><span><font>NFS</font></span><span>只需要放到</span><span><font>A</font></span><span>上，然后</span><span><font>A</font></span><span>共享给</span><span><font>B</font></span><span>和</span><span><font>C</font></span><span>即可。访问的时候，</span><span><font>B</font></span><span>和</span><span><font>C</font></span><span>是通过网络的方式去访问</span><span><font>A</font></span><span>上的那个目录的。</span><span></span></font>

<font><span>【**配置**</span>**<span><font>NFS</font></span>**<span>】</span><span></span></font>

<font><span><font><span>        </span> NFS</font></span><span>配置起来还是蛮简单的，只需要编辑配置文件</span><span><font>/etc/exports</font></span><span>即可。下面笔者先创建一个简单的</span><span><font>NFS</font></span><span>服务器。</span><span></span></font>

<span><font><font>[root@localhost ~]# **cat /etc/exports**</font></font></span>

<span><font><font>/home/<span> </span> 10.0.2.0/24(rw,sync,all_squash,anonuid=501,anongid=501)</font></font></span>

<font><span>这个配置文件就这样简单一行。共分为三部分，第一部分就是本地要共享出去的目录，第二部分为允许访问的主机（可以是一个</span><span><font>IP</font></span><span>也可以是一个</span><span><font>IP</font></span><span>段）第三部分就是小括号里面的，为一些权限选项。关于第三部分，笔者简单介绍一下：</span><span></span></font>

<font><span><font>rw</font> </span><span>：读写；</span><span></span></font>

<font><span><font>ro</font> </span><span>：只读；</span><span></span></font>

<font><span><font>sync</font> </span><span>：同步模式，内存中数据时时写入磁盘；</span><span></span></font>

<font><span><font>async</font> </span><span>：不同步，把内存中数据定期写入磁盘中；</span><span></span></font>

<font><span><font>no_root_squash</font> </span><span>：加上这个选项后，</span><span><font>root</font></span><span>用户就会对共享的目录拥有至高的权限控制，就像是对本机的目录操作一样。不安全，不建议使用；</span><span></span></font>

<font><span><font>root_squash</font> </span><span>：和上面的选项对应，</span><span><font>root</font></span><span>用户对共享目录的权限不高，只有普通用户的权限，即限制了</span><span><font>root</font></span><span>；</span><span></span></font>

<font><span><font>all_squash</font> </span><span>：不管使用</span><span><font>NFS</font></span><span>的用户是谁，他的身份都会被限定成为一个指定的普通用户身份；</span><span></span></font>

<font><span><font>anonuid/anongid</font> </span><span>：要和</span><span><font>root_squash</font> </span><span>以及</span><span> <font>all_squash</font></span><span>一同使用，用于指定使用</span><span><font>NFS</font></span><span>的用户限定后的</span><span><font>uid</font></span><span>和</span><span><font>gid</font></span><span>，前提是本机的</span><span><font>/etc/passwd</font></span><span>中存在这个</span><span><font>uid</font></span><span>和</span><span><font>gid</font></span><span>。</span><span></span></font>

<font><span>介绍了上面的相关的权限选项后，再来分析一下笔者刚刚配置的那个</span><span><font>/etc/exports</font></span><span>文件。其中要共享的目录为</span><span><font>/home</font></span><span>，信任的主机为</span><span><font>10.0.2.0/24</font></span><span>这个网段，权限为读写，同步，限定所有使用者，并且限定的</span><span><font>uid</font></span><span>和</span><span><font>gid</font></span><span>都为</span><span><font>501</font></span><span>。</span><span></span></font>

<font><span>【**使用**</span>**<span><font>NFS</font></span>**<span>】</span><span></span></font>

<font><span><span></span></span><span>当编辑完配置文件</span><span><font>/etc/exports</font></span><span>后，就该启动</span><span><font>NFS</font></span><span>服务了。启动方法为：</span><span></span></font>

<span><font><font>[root@localhost ~]# **service portmap start; service nfs start**</font></font></span>

<font><span><font>NFS</font></span><span>是依托</span><span><font>portmap</font></span><span>的，所以首先要启动</span><span><font>portmap</font></span><span>，然后启动</span><span><font>NFS</font></span><span>才能是刚才的配置生效。启动完</span><span><font>NFS</font></span><span>后，就该使用</span><span><font>NFS</font></span><span>服务了。</span><span></span></font>

<font><span><font>[root@localhost ~]# **showmount -e 127.0.0.1** </font></span><span>（用在</span><span><font>client</font></span><span>上）</span><span></span></font>

<span><font><font>Export list for 127.0.0.1:</font></font></span>

<span><font><font>/home 10.0.2.0/24</font></font></span>

<font><span>用</span><span><font>shoumount -e</font> </span><span>加</span><span><font>IP</font></span><span>就可以查看</span><span><font>NFS</font></span><span>的共享情况，上例中，就可以看到</span><span><font>127.0.0.1</font></span><span>的共享目录为</span><span><font>/home</font></span><span>，信任主机为</span><span><font>10.0.2.0/24</font></span><span>这个网段。另外这个</span><span><font>showmount</font> </span><span>命令还有一个常用的选项就是</span><span><font>-a</font></span><span>了，它的意思是，把连接本机的</span><span><font>NFS</font></span><span>的</span><span><font>client</font></span><span>全部列出。</span><span></span></font>

<font><span><font>[root@localhost ~]# **mount -t nfs 10.0.2.69:/home /mnt** </font></span><span>（</span><span><font>client</font></span><span>上）</span><span></span></font>

<font><span><font>[root@localhost ~]# **showmount -a** </font></span><span>（</span><span><font>nfs</font></span><span>服务器上）</span><span></span></font>

<span><font><font>All mount points on localhost:</font></font></span>

<span><font><font>10.0.2.69:/home</font></font></span>

<font><span>前面的</span><span><font>mount</font> </span><span>命令为挂载</span><span><font>NFS</font></span><span>共享目录，相信你能看懂这个格式。</span><span><font>showmount -a</font> </span><span>命令列出所有的</span><span><font>clinet</font></span><span>。</span><span></span></font>

<font><span><font>NFS</font></span><span>服务中还有一个常用的命令那就是</span><span><font>exportfs</font></span><span>，它的常用选项为</span><span><font>[-aruv]</font></span><span>。</span><span></span></font>

<font><span><font>-a</font> </span><span>：全部挂载或者卸载；</span><span></span></font>

<font><span><font>-r</font> </span><span>：重新挂载；</span><span></span></font>

<font><span><font>-u</font> </span><span>：卸载某一个目录；</span><span></span></font>

<font><span><font>-v</font> </span><span>：显示共享的目录；</span><span></span></font>

<font><span>使用</span><span><font>exportfs</font></span><span>命令，当改变</span><span><font>/etc/exports</font></span><span>配置文件后，不用重启</span><span><font>nfs</font></span><span>服务直接用这个</span><span><font>exportfs</font></span><span>即可。</span><span></span></font>

<span><font><font>[root@localhost ~]# **cat /etc/exports**</font></font></span>

<font><font><span>/tmp/<span>  </span> 10.0.2.0/24(rw,sync,no_root_squash)</span><span></span></font></font>

<font><span><font>[root@localhost ~]# **exportfs -arv** </font></span><span>（</span><span><font>nfs</font></span><span>服务器上）</span><span></span></font>

<span><font><font>exporting 10.0.2.0/24:/tmp</font></font></span>

<font><span>更改目录后，直接</span><span><font>exportfs -arv</font></span><span>即可生效。</span><span></span></font>

<font><span>在上面使用到了</span><span><font>mount</font></span><span>命令来挂载</span><span><font>nfs</font></span><span>，其实</span><span><font>mount</font></span><span>这个</span><span><font>nfs</font></span><span>服务还是有些说法的。首先是用</span><span><font>-t nfs</font> </span><span>来指定挂载的类型为</span><span><font>nfs</font></span><span>。另外在使用</span><span><font>nfs</font></span><span>时，常用一个选项就是</span><span><font>nolock</font></span><span>了，即在挂载</span><span><font>nfs</font></span><span>服务时，不加锁。</span><span></span></font>

<span><font><font>[root@localhost ~]# **mount -t nfs -o nolock 10.0.2.69:/tmp /mnt/**</font></font></span>

<span><font><font>[root@localhost ~]# **showmount -a**</font></font></span>

<span><font><font>All mount points on localhost:</font></font></span>

<span><font><font>10.0.2.69:/home</font></font></span>

<span><font><font>10.0.2.69:/tmp</font></font></span>

<font><span>另外我们还可以把要挂载的</span><span><font>nfs</font></span><span>目录写到</span><span><font>client</font></span><span>上的</span><span><font>/etc/fstab</font></span><span>文件中，挂载时只需要</span><span><font>mount -a</font></span><span>即可。</span><span></span></font>

<span><font><font>[root@localhost ~]# **cat /etc/fstab**</font></font></span>

<span><font><font>LABEL=/<span>                </span> /<span>                      </span> ext3<span>   </span> defaults<span>       </span> 1 1</font></font></span>

<span><font><font>LABEL=/boot<span>            </span> /boot<span>                  </span> ext3<span>   </span> defaults<span>       </span> 1 2</font></font></span>

<span><font><font>tmpfs<span>                  </span> /dev/shm<span>               </span> tmpfs<span>  </span> defaults<span>       </span> 0 0</font></font></span>

<span><font><font>devpts<span>                 </span> /dev/pts<span>               </span> devpts<span> </span> gid=5,mode=620<span> </span> 0 0</font></font></span>

<span><font><font>sysfs<span>                  </span> /sys<span>                   </span> sysfs<span>  </span> defaults<span>       </span> 0 0</font></font></span>

<span><font><font>proc<span>                   </span> /proc<span>                  </span> proc<span>   </span> defaults<span>       </span> 0 0</font></font></span>

<span><font><font>LABEL=SWAP-hda2<span>        </span> swap<span>     </span> <span>              </span>swap<span>   </span> defaults<span>       </span> 0 0</font></font></span>

<span><font><font>10.0.2.69:/tmp<span>         </span> /mnt<span>                   </span> nfs<span>    </span> nolock<span>         </span> 0 0</font></font></span>

<span></span>

<font><span>写完</span><span><font>/etc/fstab</font></span><span>文件后，只需要</span><span><font>mount -a</font></span><span>即可挂载</span><span><font>nfs</font></span><span>服务的共享目录。</span><span></span></font>

<font><span><font>[root@localhost ~]# **umount /mnt/**</font> </span><span>首先把刚才挂载的</span><span><font>nfs</font></span><span>卸载掉</span><span></span></font>

<span><font><font>[root@localhost ~]# **mount -a**</font></font></span>

<span><font><font>[root@localhost ~]# **df -h**</font></font></span>

<span><font><font>Filesystem<span>           </span> Size<span> </span> Used Avail Use% Mounted on</font></font></span>

<span><font><font>/dev/hda3<span>            </span> 7.3G<span> </span> 3.7G<span> </span> 3.3G<span> </span> 53% /</font></font></span>

<span><font><font>/dev/hda1<span>             </span> 99M<span>  </span> 12M<span>  </span> 83M<span> </span> 12% /boot</font></font></span>

<span><font><font>tmpfs<span>                 </span> 84M<span>    </span> 0<span>  </span> 84M<span>  </span> 0% /dev/shm</font></font></span>

<span><font><font>10.0.2.69:/tmp<span>       </span> 7.3G<span> </span> 3.7G<span> </span> 3.3G<span> </span> 53% /mnt</font></font></span>

<font><span>关于</span><span><font>NFS</font></span><span>部分就讲这么多，内容并不多，相信你很快就能掌握！</span></font><span></span>

