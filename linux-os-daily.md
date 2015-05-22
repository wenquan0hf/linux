# linux 系统日常管理 

<span>笔者在前面介绍的内容都为</span><span>linux</span><span>系统基础类的，如果你现在把前面的内容全部很好的掌握了，那最好了</span><span>。</span><span>不过笔者要说的是，即使你完全掌握了，你现在还是不能作为一名合格的</span><span>linux</span><span>系统管理员的，毕竟系统管理员要会做的事情太多了</span><span>。</span><span>本章以及后面章节笔者会陆续教给你作为</span><span>linux</span><span>系统管理员所必备的知识</span><span>。</span><span>只要你熟练掌握那绝对可以胜任一个最初级的管理员职位，不过只是初级的，因为你还需要在日常的管理工作中获得成长</span><span>。</span>

<span>**【**</span><span>**监控系统的状态**</span><span>**】**</span>

<span>**1\. w** </span><span>**查看当前系统的负载**</span>

<span>![15_1.png.jpg](images/15_1.png.jpg)</span>

<span>相信所有的</span><span>linux</span><span>管理员最常用的命令就是这个</span><span>’w’</span> <span>了，该命令显示的信息还是蛮丰富的</span><span>。</span><span>第一行从左面开始显示的信息依次为：时间，系统运行时间，登录用户数，平均负载</span><span>。</span><span>第二行开始以及下面所有的行，告诉我们的信息是，当前登录的都有哪些用户，以及他们是从哪里登录的等等</span><span>。</span><span>其实，在这些信息当中，笔者认为我们最应该关注的应该是第一行中的</span><span>’load average:’</span><span>后面的三个数值</span><span>。</span>

<span>第一个数值表示</span><span>1</span><span>分钟内系统的平均负载值；第二个数值表示</span><span>5</span><span>分钟内系统的平均负载值；第三个数值表示</span><span>15</span><span>分钟系统的平均负载值</span><span>。</span><span>这个值的意义是，单位</span><span>时间</span><span>段内</span><span>CPU</span><span>活动</span><span>进程</span><span>数</span><span>。</span><span>当然这个值越大就说明你的</span><span>服务器</span><span>压力越大</span><span>。</span><span>一般情况下这个值只要不超过你</span><span>服务</span><span>器的</span><span>cpu</span><span>数量就没有关系，如果你的服务器</span><span>cpu</span><span>数量为</span><span>8</span><span>，那么这个值若小于</span><span>8</span><span>，就说明你的服务器没有压力，否则就要关注一下了</span><span>。</span><span>到这里你肯定会问，如何查看服务器有几个</span><span>cpu</span><span>？</span>

<span>![15_7.png.jpg](images/15_7.png.jpg)</span>

<span>就是用这个命令了</span><span>。’/proc/cpuinfo’</span><span>这个文件记录了</span><span>cpu</span><span>的详细信息</span><span>。</span><span>目前市面上的服务器通常都是</span><span>2</span><span>颗</span><span>4</span><span>核</span><span>cpu</span><span>，在</span><span>linux</span><span>看来，它就是</span><span>8</span><span>个</span><span>cpu。</span><span>查看这个文件时则会显示</span><span>8</span><span>段类似的信息，而最后一段信息中</span><span>processor :</span> <span>后面跟的是</span><span>’7’。</span><span>所以查看当前系统有几个</span><span>cpu</span><span>，你可以使用这个命令：</span><span>’ grep -c 'processor' /proc/cpuinfo’ 。</span>

![15_8.png.jpg](images/15_8.png.jpg)

<span>**2\. vmstat** </span><span>**监控系统的状态**</span>

<span>![15_9.png.jpg](images/15_9.png.jpg)</span>

<span>上面讲的</span><span>w</span><span>查看的是系统整体上的负载，通过看那个数值可以知道当前系统有没有压力，但是具体是哪里（</span><span>CPU,</span> <span>内存，磁盘等）有压力就无法判断了</span><span>。</span><span>通过</span><span>vmstat</span><span>就可以知道具体是哪里有压力</span><span>。vmstat</span><span>命令打印的结果共分为</span><span>6</span><span>部分：</span><span>procs, memory, swap, io, system, cpu.</span><span>请重点关注一下红色标出的项</span><span>。</span>

<span>1</span><span>）</span><span>procs</span> <span>显示进程相关信息</span>

<span>r</span><span>：表示运行和等待</span><span>cpu</span><span>时间</span><span>片的</span><span>进程</span><span>数，如果长期大于服务器</span><span>cpu</span><span>的个数，则说明</span><span>cpu</span><span>不够用了；</span>

<span>b</span><span>：表示等待资源的进程数，比如等待</span><span>I/O,</span> <span>内存等，这列的值如果长时间大于</span><span>1</span><span>，则需要你关注一下了；</span>

<span>2</span><span>）</span><span>memory</span> <span>内存相关信息</span>

<span>swpd</span> <span>：表示切换到交换分区中的内存数量</span><span>；</span>

<span>free</span> <span>：当前空闲的内存数量；</span>

<span>buff</span> <span>：缓冲大小，（即将写入磁盘的）；</span>

<span>cache</span> <span>：缓存大小，（从磁盘中读取的）；</span>

<span>3</span><span>）</span><span>swap</span> <span>内存交换情况</span>

<span>si</span> <span>：由内存进入交换区的数量；</span>

<span>so</span><span>：由交换区进入内存的数量；</span>

<span>4</span><span>）</span><span>io</span> <span>磁盘使用情况</span>

<span>bi</span> <span>：从块设备读取数据的量（读磁盘）；</span>

<span>bo</span><span>：</span><span>从块设备写入数据的量（写磁盘）；</span>

<span>5</span><span>）</span><span>system</span> <span>显示采集间隔内发生的中断次数</span>

<span>in</span> <span>：表示在某一时间间隔中观测到的每秒设备中断数；</span>

<span>cs</span> <span>：表示每秒产生的上下文切换次数；</span>

<span>6</span><span>）</span><span>CPU</span> <span>显示</span><span>cpu</span><span>的使用状态</span>

<span>us</span> <span>：显示了</span><span>用户</span><span>下所花费</span> <span>cpu</span> <span>时间的百分比；</span>

<span>sy</span> <span>：显示系统花费</span><span>cpu</span><span>时间百分比；</span>

<span>id</span> <span>：表示</span><span>cpu</span><span>处于空闲状态的时间百分比；</span>

<span>wa</span><span>：表示</span><span>I/O</span><span>等待所占用</span><span>cpu</span><span>时间百分比；</span>

<span>st</span> <span>：表示被偷走的</span><span>cpu</span><span>所占百分比（一般都为</span><span>0</span><span>，不用关注）；</span>

<span>以上所介绍的各个参数中，笔者经常会关注</span><span>r</span><span>列，</span><span>b</span><span>列，和</span><span>wa</span><span>列，三列代表的含义在上边说得已经很清楚</span><span>。IO</span><span>部分的</span><span>bi</span><span>以及</span><span>bo</span><span>也是我要经常参考的对象</span><span>。</span><span>如果磁盘</span><span>io</span><span>压力很大时，这两列的数值会比较高</span><span>。</span><span>另外当</span><span>si, so</span><span>两列的数值比较高，并且在不断变化时，说明内存不够了，内存中的数据频繁交换到交换分区中，这往往对系统性能影响极大</span><span>。</span>

<span>![15_10.png.jpg](images/15_10.png.jpg)</span>

<span>笔者用</span><span>vmstat</span><span>时，经常用这样的形式，</span><span>’vmstat 1 5’</span> <span>表示每隔</span><span>1</span><span>秒钟打印一次系统状态，连续打印</span><span>5</span><span>次</span><span>。</span><span>当然你也可以</span> <span>‘vmstat 1 ‘</span> <span>表示每隔</span><span>1</span><span>秒钟打印一次系统状态，一直打印，除非你按</span><span>ctrl + c</span><span>强制结束</span><span>。</span>

<span>**3\. top** </span><span>**显示进程所占系统资源**</span>

<span>![15_11.png.jpg](images/15_11.png.jpg)</span>

<span>这个命令用于动态监控进程所占系统资源，每隔</span><span>3</span><span>秒变一次</span><span>。</span><span>这个命令的特点是把占用系统资源（</span><span>CPU</span><span>，内存，磁盘</span><span>IO</span><span>等）最高的进程放到最前面</span><span>。top</span><span>命令打印出了很多信息，包括系统负载（</span><span>load average</span><span>）</span><span>、</span><span>进程数（</span><span>Tasks</span><span>）</span><span>、cpu</span><span>使用情况</span><span>、</span><span>内存使用情况以及交换分区使用情况</span><span>。</span><span>其实上面这些内容可以通过其他命令来查看，所以用</span><span>top</span><span>重点查看的还是下面的进程使用系统资源详细状况</span><span>。</span><span>这部分东西反映的东西还是比较多的，不过需要你关注的也就是几项：</span><span>%CPU, %MEM, COMMAND</span> <span>这些项目所代表的意义，不用笔者介绍相信你也能看懂吧</span><span>。</span>

<span>![15_21.png.jpg](images/15_21.png.jpg)</span>

<span>另外笔者使用</span><span>top</span><span>命令时还常常使用</span><span>-bn1</span> <span>这个组合选项，它表示非动态打印系统资源使用情况，可以用在脚本中，你不妨记一下，以后也许你会用得到</span><span>。</span>

<span>**4\. sar** </span><span>**监控系统状态**</span>

<span>sar</span> <span>命令很强大，它可以监控系统所有资源状态，比如平均负载</span><span>、</span><span>网卡流量</span><span>、</span><span>磁盘状态</span><span>、</span><span>内存使用等等</span><span>。</span><span>它不同于其他系统状态监控工具的地方在于，它可以打印历史信息，可以显示当天从零点开始到当前时刻的系统状态信息</span><span>。</span><span>如果你系统没有安装这个命令，请使用</span><span>”yum install -y sysstat”</span><span>命令安装</span><span>。</span><span>初次使用</span><span>sar</span><span>命令会报错，那是因为</span><span>sar</span><span>工具还没有生成相应的数据库文件（时时监控就不会了，因为不用去查询那个库文件）</span><span>。</span><span>它的数据库文件在</span><span>” /var/log/sa/”</span><span>目录下，默认保存</span><span>9</span><span>天</span><span>。</span><span>因为这个命令太过复杂，所以笔者只介绍几个</span><span>。</span>

<span>**1**</span><span>**）查看网卡流量**</span><span> **‘sar -n DEV ‘**</span>

<span>![15_22.png.jpg](images/15_22.png.jpg)</span>

<span>IFACE</span><span>这列表示设备名称，</span><span>rxpck/s</span> <span>表示每秒进入收取的包的数量，</span><span>txpck/s</span> <span>表示每秒发送出去的包的数量，</span><span>rxbyt/s</span> <span>表示每秒收取的数据量（单位</span><span>Byte</span><span>），</span><span>txbyt/s</span><span>表示每秒发送的数据量</span><span>。</span><span>后面几列不需要关注</span><span>。</span><span>如果有一天你所管理的服务器丢包非常严重，那么你就应该看一看这个网卡流量是否异常了，如果</span><span>rxpck/s</span> <span>那一列的数值大于</span><span>4000</span><span>，或者</span><span>rxbyt/s</span><span>那列大于</span><span>5,000,000</span><span>则很有可能是被攻击了</span><span>，正常的服务器网卡流量不会高于这么多，除非是你自己在拷贝数据</span><span>。</span><span>上面的命令是查看网卡流量历史的，如何时时查看网卡流量呢？</span>

<span>![15_23.png.jpg](images/15_23.png.jpg)</span>

<span>另外也可以查看某一天的网卡流量历史，使用</span><span>-f</span><span>选项，后面跟文件名，如果你的系统格式</span><span>Redhat</span><span>或者</span><span>CentOS</span><span>那么</span><span>sar</span><span>的库文件一定是在</span><span>/var/log/sa/</span><span>目录下的</span><span>。</span>

<span>![15_24.png.jpg](images/15_24.png.jpg)</span>

<span>**2**</span><span>**）查看历史负载**</span><span> **‘sar -q’**</span>

<span>![15_25.png.jpg](images/15_25.png.jpg)</span>

<span>这个命令有助于我们查看服务器在过去的某个时间的负载状况</span><span>。</span>

<span>关于</span><span>sar</span><span>的介绍笔者不愿写太多，毕竟介绍太多会给你带来更多的压力，其实笔者介绍这个命令的目的只是让你学会查看网卡流量（这是非常有用的）</span><span>。</span><span>如果你很感兴趣那就</span><span>man</span><span>一下吧，它的用法太多了</span><span>。</span>

<span>**5\. free**</span><span>**查看内存使用状况**</span>

<span>![15_26.png.jpg](images/15_26.png.jpg)</span>

<span>只要你敲一个</span><span>free</span><span>然后回车就可以当前系统的总内存大小以及使用内存的情况</span><span>。</span><span>从上图中可看到当前系统内存总大小为</span><span>235128</span><span>（单位是</span><span>k</span><span>）已经使用</span><span>120368</span><span>，剩余</span><span>94760。</span><span>其实真正剩余并不是这个</span><span>94760</span><span>，而是第二行的</span><span>213388</span><span>，真正使用的也是第二行的</span><span>21740。</span><span>这是因为系统初始化时，就已经分配出很大一部分内存给</span><span>缓存</span><span>，这部分缓存用来随时提供给程序使用，如果程序不用，那这部分内存就空闲</span><span>。</span><span>所以，</span><span>查看内存使用多少，剩余多少请看第二行的数据</span><span>。</span><span>另外你还可以加</span><span>-m</span> <span>或者</span><span>-g</span><span>选项分别以</span><span>M</span><span>或</span><span>G</span><span>为单位打印内存使用状况</span><span>。</span>

<span>![15_27.png.jpg](images/15_27.png.jpg)</span>

<span>**6\. ps** </span><span>**查看系统进程**</span>

<span>作为系统管理员，一定要知道你所管理的系统都有那些进程在运行，在</span><span>windows</span><span>下只要打开任务管理器即可查看</span><span>。</span><span>在</span><span>linux</span><span>下呢？其实在上面介绍的</span><span>top</span><span>命令就可以，但是不够专业，当然还有专门显示系统进程的命令</span><span>。</span>

<span>![15_28.png.jpg](images/15_28.png.jpg)</span>

<span>对了，就是这个</span><span>’ps aux’。</span><span>笔者也经常看到有的人喜欢用</span><span>’ps -elf’</span> <span>大同小异，显示的信息基本上是一样的</span><span>。 ps</span><span>命令还有更多的用法，笔者不再做介绍，因为你只要会用这个命令就足够了，请</span><span>man</span><span>一下</span><span>。</span><span>下面介绍上图上出现的几个参数的意义</span><span>。</span>

<span>**PID**</span><span>：进程的</span><span>id</span><span>，这个</span><span>id</span><span>很有用，在</span><span>linux</span><span>中内核管理进程就得靠</span><span>pid</span><span>来识别和管理某一个程，比如我想终止某一个进程，则用</span> <span>‘kill</span> <span>进程的</span><span>pid’</span><span>，有时并不能杀掉，则需要加一个</span><span>-9</span><span>选项了</span><span>’kill -9</span> <span>进程</span><span>pid’</span>

<span>**STAT** </span><span>：表示进程的状态，进程状态分为以下几种（</span><span>不要求记住，但要了解</span><span>）</span>

<span>D  </span><span>不能中断的进程（通常为</span><span>IO</span><span>）</span>

<span>R  </span><span>正在运行中的进程</span>

<span>S  </span><span>已经中断的进程，通常情况下，系统中大部分进程都是这个</span><span>状态</span>

<span>T  </span><span>已经停止或者暂停的进程，如果我们正在运行一个</span><span>命令</span><span>，比如说</span><span>sleep 10</span><span>，如果我们按一下</span><span>ctrl -z</span> <span>让他暂停，那么我们用</span><span>ps</span><span>查看就会显示</span><span>T</span><span>这个状态</span>

<span>W</span> <span>这个好像是说，从内核</span><span>2.6xx</span> <span>以后，表示为没有足够的内存页分配</span>

<span>X  </span><span>已经死掉的进程（这个好像从来不会出现）</span>

<span>Z  </span><span>僵尸进程，杀不掉，打不死的垃圾进程，占系统一小点资源，不过没有关系</span><span>。</span><span>如果太多，就有问题了</span><span>。</span><span>一般不会出现</span><span>。</span>

<span><  </span><span>高优先级进程</span>

<span>N  </span><span>低优先级进程</span>

<span>L   </span><span>在内存中被锁了内存分页</span>

<span>s   </span><span>主进程</span>

<span>l   </span><span>多线程进程</span>

<span>+  </span><span>代表在前台运行的进程</span>

<span>这个</span><span>ps</span><span>命令是笔者在工作中用的非常多的命令之一，所以请记住它吧</span><span>。</span><span>关于</span><span>ps</span><span>命令的使用，笔者经常会连同管道符一起使用，用来查看某个进程或者它的数量</span><span>。</span>

<span>![15_29.png.jpg](images/15_29.png.jpg)</span>

<span>上面的</span><span>6</span><span>不对，需要减掉</span><span>1</span><span>，因为使用</span><span>grep</span><span>命令时，</span><span>grep</span><span>命令本身也算作了一个</span><span>。</span>

<span>**7\. netstat** </span><span>**查看网络状况**</span>

<span>![15_44.png.jpg](images/15_44.png.jpg)</span>

<span>netstat</span><span>命令用来打印网络连接状况</span><span>、</span><span>系统所开放端口</span><span>、</span><span>路由表等信息</span><span>。</span><span>笔者最常用的关于</span><span>netstat</span><span>的命令就是这个</span><span>netstat -lnp</span><span>（打印当前系统启动哪些端口）以及</span><span>netstat -an</span> <span>（打印网络连接状况）这两个命令非常有用，请一定要记住</span><span>。</span>

<span>![15_45.png.jpg](images/15_45.png.jpg)</span>

<span>如果你所管理的服务器是一台提供</span><span>web</span><span>服务（</span><span>80</span><span>端口）的服务器，那么你就可以使用</span><span>netstat -an |grep 80</span><span>开查看当前连接</span><span>web</span><span>服务的有哪些</span><span>IP</span><span>了</span><span>。</span>

<span>**8\.** </span><span>**抓包工具**</span><span>**tcpdump**</span>

<span>有时候，也许你会有这样的需求，想看一下某个网卡上都有哪些数据包，尤其是当你初步判定你的服务器上有流量攻击</span><span>。</span><span>这时，使用抓包工具来抓一下数据包，就可以知道有哪些</span><span>IP</span><span>在攻击你了</span><span>。</span>

<span>![15_46.png.jpg](images/15_46.png.jpg)</span>

<span>如果你没有</span><span>tcpdump</span> <span>这个命令，需要用</span><span>’yum install -y tcpdump ’</span><span>命令去安装一下</span><span>。</span><span>上图中第三列和第四列显示的信息为哪一个</span><span>IP+port</span><span>在连接哪一个</span><span>IP+port</span><span>，后面的信息是该数据包的相关信息，如果不懂也没有关系，毕竟你不是专门搞网络的，而这里需要你关注的只是第三列以及第四列</span><span>。-i</span> <span>选项后面跟设备名称，如果你想抓</span><span>eth1</span><span>网卡的包，后面则要跟</span><span>eth1.</span><span>至于</span><span>-nn</span><span>选项的作用是让第三列和第四列显示成</span><span>IP+</span><span>端口号的形式，如果不加</span><span>-nn</span><span>则显示的是主机名</span><span>+</span><span>服务名称</span><span>。</span>

<span>**【linux**</span><span>**网络相关**</span><span>**】**</span>

<span>**1\. ifconfig** </span><span>**查看网卡**</span><span>**IP**</span>

<span>ifconfig</span><span>类似与</span><span>windows</span><span>的</span><span>ipconfig</span><span>，不加任何选项和参数只打印当前网卡的</span><span>IP</span><span>相关信息（子网掩码</span><span>、</span><span>网关等）</span>

<span>![15_47.png.jpg](images/15_47.png.jpg)</span>

<span>当然</span><span>ifconfig</span><span>后面可以跟设备名，只打印指定设备的</span><span>IP</span><span>信息</span><span>。</span>

<span>![15_48.png.jpg](images/15_48.png.jpg)</span>

<span>在</span><span>windows</span><span>下设置</span><span>IP</span><span>非常简单，然而在命令窗口下如何设置？这就需要去修改配置文件</span><span>/etc/sysconfig/network-scripts/ifcfg-eth0</span><span>了，如果是</span><span>eth1</span><span>那么配置文件是</span><span>/etc/sysconfig/network-scripts/ifcfg-eth1.</span>

<span>![15_49.png.jpg](images/15_49.png.jpg)</span>

<span>如果想修改</span><span>IP</span><span>的话，则只需要修改</span><span>IPADDR , NETMASK</span><span>以及</span><span>GATEWAY</span><span>即可</span><span>。</span><span>如果你的</span><span>linux</span><span>是通过</span><span>dhcp</span><span>服务器自动获得的</span><span>IP</span><span>，那么配置文件肯定和上图中的不一样，</span><span>BOOTPROTO</span><span>那里会是</span><span>’dhcp’</span><span>，如果你要配置成静态</span><span>IP</span><span>的话，这里就需要写成</span><span>’none’。</span><span>关于如何设置</span><span>IP</span><span>以及子网掩码的这些知识属于网络相关的基础知识了，如果你对这方面比较陌生的话，建议你去看看网络相关的资料</span><span>。</span><span>当修改完</span><span>IP</span><span>后需要重启网络服务新</span><span>IP</span><span>才能生效，重启命令为</span><span>’ service network restart’</span>

<span>![15_50.png.jpg](images/15_50.png.jpg)</span>

<span>另外如果你有多个网卡的情况时，只想重启某一个网卡的话，还可以使用这个命令</span><span>。</span>

<span>![15_51.png.jpg](images/15_51.png.jpg)</span>

<span>ifdown</span> <span>即停掉网卡，</span><span>ifup</span><span>即启动网卡</span><span>。</span><span>有一点要提醒你的是，如果你远程登录你的服务器，当你使用</span><span>ifdown eth0</span><span>这个命令的时候，很有可能后面的命令</span><span>ifup eth0</span><span>不会被运行，这样导致你断网而无法连接服务器，所以请尽量使用</span><span>service network restart</span> <span>这个命令来重启网卡</span><span>。</span>

<span>**2\.** </span><span>**给一个网卡设定多个**</span><span>**IP**</span>

<span>在</span><span>linux</span><span>系统中，网卡是可以设定多重</span><span>IP</span><span>的，笔者曾经管理的一台服务器的</span><span>eth1</span><span>就设定了</span><span>5</span><span>个</span><span>IP</span><span>，实在是够变态的</span><span>。</span>

<span>![15_52.png.jpg](images/15_52.png.jpg)</span>

<span>把</span><span>ifcfg-eth0</span><span>复制成</span><span>ifcfg-eth0:1</span> <span>然后编辑</span><span>ifcfg-eth0:1</span><span>修改</span><span>DEVICE</span><span>以及</span><span>IPADDR</span><span>保存后重启网卡</span><span>。</span>

<span>![15_53.png.jpg](images/15_53.png.jpg)</span>

<span>再次查看</span><span>eth0</span><span>上就有两个</span><span>IP</span><span>了</span><span>。</span><span>这里你要注意一下，文件名（</span><span>ifcft-eth0:1</span><span>）写成什么都无所谓，但是文件内的</span><span>DEVICE=eth0:1</span><span>一定要按照这样的格式写，否则你启动不起来网卡</span><span>。</span>

<span>**3\.** </span><span>**查看网卡连接状态**</span>

<span>![15_54.png.jpg](images/15_54.png.jpg)</span>

<span>mii-tool</span><span>这个命令用来查看网卡是否连接，如图显示</span><span>link ok</span><span>等字样说明连接正常，否则会显示</span><span>’</span><span>no link</span><span>’</span><span>字样，下图是笔者所管理的一台服务器，</span><span>eth1</span><span>网卡没有连接</span><span>。</span>

<span>![15_55.png.jpg](images/15_55.png.jpg)</span>

<span>如果你的机器是虚拟机，那么你使用该命令时应该显示成如下：</span>

<span>![15_56.png.jpg](images/15_56.png.jpg)</span>

<span>这是因为使用的是虚拟网卡，不支持这个工具查看</span><span>。</span><span>不用多关注此，你记住这个</span><span>mii-tool</span><span>命令即可，它可是会经常用到的</span><span>。</span>

<span>**4\.** </span><span>**更改主机名**</span>

<span>当装完系统后，默认主机名为</span><span>localhost</span><span>，使用</span><span>hostname</span><span>就可以知道你的</span><span>linux</span><span>的主机名是什么</span><span>。</span>

<span>![15_57.png.jpg](images/15_57.png.jpg)</span><span>同样使用</span><span>hostname</span><span>可以更改你的主机名</span><span>。</span>

<span>![15_71.png.jpg](images/15_71.png.jpg)</span>

<span>下次登录时就会把命令提示符</span><span>![15_72.png.jpg](images/15_72.png.jpg)</span><span>中的</span><span>’localhost’</span><span>更改成</span><span>’Aming’。</span><span>不过这样修改只是保存在内存中，下次重启还会变成未改之前的主机名，所以需要你还要去更改相关的配置文件</span><span>’/etc/sysconfig/network’。</span>

<span>![15_73.png.jpg](images/15_73.png.jpg)</span>

<span>把</span><span>HOSTNAME=localhost.localdomain</span> <span>修改成你想要的主机名，这样再重启就会读取这个配置文件中的</span><span>HOSTNAME.</span>

<span>**5\.** </span><span>**设置**</span><span>**DNS**</span>

<span>DNS</span><span>是用来解析域名用的，平时我们访问网站都是直接输入一个网址，而</span><span>dns</span><span>把这个网址解析到一个</span><span>IP。</span><span>关于</span><span>dns</span><span>的概念，如果你很陌生的话，那就去网上查一下吧</span><span>。</span><span>在</span><span>linux</span><span>下面设置</span><span>dns</span><span>非常简单，只要把</span><span>dns</span><span>地址写到一个配置文件中即可</span><span>。</span><span>这个配置文件就是</span><span>/etc/resolv.conf</span>

<span>![15_74.png.jpg](images/15_74.png.jpg)</span>

<span>resolv.conf</span><span>有它固有的格式，一定要写成</span><span>’nameserver IP’</span><span>的格式，上面那行以</span><span>’;’</span><span>为开头的行是一行注释，没有实际意义，建议写两个或多个</span><span>namserver</span> <span>，默认会用第一个</span><span>namserver</span><span>去解析域名，当第一个解析不到时会使用第二个</span><span>。</span><span>在</span><span>linux</span><span>下面有一个特殊的文件</span><span>/etc/hosts</span><span>也能解析域名，不过是需要我们手动在里面添加</span><span>IP+</span><span>域名这些内容，它的作用是临时解析某个域名，非常有用</span><span>。</span>

<span>![15_75.png.jpg](images/15_75.png.jpg)</span>

<span>它的格式如上图，每一行作为一条记录，分成两部分，第一部分是</span><span>IP</span><span>，第二部分是域名</span><span>。</span><span>关于</span><span>hosts</span><span>文件，有几点需要你注意：</span>

<span>1</span><span>）一个</span><span>IP</span><span>后面可以跟多个域名，可以是几十个甚至上百个；</span>

<span>2</span><span>）每行只能有一个</span><span>IP</span><span>，也就是说一个域名不能对应多个</span><span>IP</span><span>；</span>

<span>3</span><span>）如果有多行中出现相同的域名（前面</span><span>IP</span><span>不一样），会按最前面出现的记录来解析</span><span>。</span>

<span>【</span><span>**linux**</span><span>**的防火墙**</span><span>】</span>

<span>**1\. selinux**</span>

<span>Selinux</span><span>是</span><span>Redhat/CentOS</span><span>系统特有的安全机制</span><span>。</span><span>不过因为这个东西限制太多，配置也特别繁琐所以几乎没有人去真正应用它</span><span>。</span><span>所以装完系统，我们一般都要把</span><span>selinux</span><span>关闭，以免引起不必要的麻烦</span><span>。</span><span>关闭</span><span>selinux</span><span>的方法为：</span>

<span>![15_76.png.jpg](images/15_76.png.jpg)</span>

<span>把</span><span>’SELINUX=enforcing’</span><span>改成</span><span>’SELINUX=disabled’</span><span>，然后重启机器</span><span>。</span><span>临时关闭</span><span>selinux</span><span>的命令为</span>

<span>![15_77.png.jpg](images/15_77.png.jpg)</span>

<span>getenforce</span><span>命令可以得到</span><span>selinux</span><span>的状态，其中有两种（</span><span>Enforcing|Permissive</span><span>），前者表示开放，后者表示关闭，但是会发出警告</span><span>。setenforce</span><span>用来设置</span><span>selinux</span><span>的状态，后面跟</span><span>0</span><span>则设置成</span><span>Permissive</span><span>后面跟</span><span>1</span><span>设置成</span><span>Enforcing。</span><span>关闭</span><span>selinux</span><span>的命令为</span><span>setenforce 0</span><span>，但是这只是临时关闭，重启后恢复，想要永久生效，请更改配置文件</span><span>/etc/selinux/config。</span>

<span>**2\. iptables**</span>

<span>Iptables</span><span>是</span><span>linux</span><span>上特有的防火墙机制，其功能非常强大，然而笔者在日常的管理工作中仅仅用到了一两个应用，这并不代表</span><span>iptables</span><span>不重要</span><span>。</span><span>作为一个网络管理员，</span><span>iptables</span><span>是必要要熟练掌握的</span><span>。</span><span>但是作为系统管理员，我们也应该会最基本的</span><span>iptables</span><span>操作，认识</span><span>iptables</span><span>的基本规则</span><span>。</span>

<span>**1**</span><span>**）**</span><span>**iptalbes**</span><span>**的三个表**</span>

<span>filter</span> <span>：这个表主要用于过滤包的，是系统预设的表，这个表也是笔者用的最多的</span><span>。</span><span>内建三个链</span><span>INPUT、OUTPUT</span><span>以及</span><span>FORWARD。INPUT</span><span>作用于进入本机的包；</span><span>OUTPUT</span><span>作用于本机送出的包；</span><span>FORWARD</span><span>作用于那些跟本机无关的包</span><span>。</span>

<span>nat</span> <span>：主要用处是网络地址转换，也有三个链</span><span>。</span><span>PREROUTING</span> <span>链的作用是在包刚刚到达防火墙时改变它的目的地址，如果需要的话</span><span>。OUTPUT</span><span>链改变本地产生的包的目的地址</span><span>。POSTROUTING</span><span>链在包就要离开防火墙之前改变其源地址</span><span>。</span><span>该表笔者用的不多，但有时候会用到</span><span>。</span>

<span>mangle</span> <span>：这个表主要是用于给数据包打标记，然后根据标记去操作哪些包</span><span>。</span><span>这个表几乎不怎么用</span><span>。</span><span>除非你想成为一个高级网络工程师，否则你就没有必要花费很多心思在它上面</span><span>。</span>

<span>**2**</span><span>**）**</span><span>**iptables** </span><span>**基本语法**</span>

<span>**A.** </span><span>**查看规则以及清除规则**</span>

<span>![15_78.png.jpg](images/15_78.png.jpg)</span>

<span>如上图，</span><span>-t</span> <span>后面跟表名，</span><span>-nvL</span> <span>即查看该表的规则，其中</span><span>-n</span><span>表示不针对</span><span>IP</span><span>反解析主机名；</span><span>-L</span><span>表示列出的意思；而</span><span>-v</span><span>表示列出的信息更加详细</span><span>。</span><span>如果不加</span><span>-t</span> <span>，则打印</span><span>filter</span><span>表的相关信息</span><span>。</span>

<span>![15_79.png.jpg](images/15_79.png.jpg)</span>

<span>这个和</span><span>-t filter</span> <span>打印的信息是一样的</span><span>。</span>

<span>关于清除规则的命令中，笔者用的最多就是</span>

<span>![15_80.png.jpg](images/15_80.png.jpg)</span>

<span>不加</span><span>-t</span><span>默认是针对表</span><span>filter</span><span>来操作的，</span><span>-F</span> <span>表示把所有规则全部删除；</span><span>-Z</span><span>表示把包以及流量计数器置零（这个笔者认为很有用）</span><span>。</span>

<span>**B.** </span><span>**增加**</span><span>**/**</span><span>**删除一条规则**</span>

<span>![15_81.png.jpg](images/15_81.png.jpg)</span>

<span>这就是增加了一条规则，省略</span><span>-t</span><span>所以针对的是</span><span>filter</span><span>表</span><span>。-A</span> <span>表示增加一条规则，另外还有</span><span>-I</span> <span>表示插入一条规则，</span><span>-D</span><span>删除一条规则；后面的</span><span>INPUT</span><span>即链名称，还可以是</span><span>OUTPUT</span><span>或者</span><span>FORWORD</span><span>；</span><span>-s</span> <span>后跟源地址；</span><span>-p</span> <span>协议（</span><span>tcp, udp, icmp</span><span>）；</span> <span>--sport/--dport</span> <span>后跟源端口</span><span>/</span><span>目标端口；</span><span>-d</span> <span>后跟目的</span><span>IP</span><span>（主要针对内网或者外网）；</span><span>-j</span> <span>后跟动作（</span><span>DROP</span><span>即把包丢掉，</span><span>REJECT</span><span>即包拒绝；</span><span>ACCEPT</span><span>即允许包）</span><span>。</span><span>这样讲可能很乱，那笔者多举几个例子来帮你理解：</span>

<span>![15_82.png.jpg](images/15_82.png.jpg)</span>

<span>上例表示：插入一条规则，把来自</span><span>10.0.2.36</span><span>的所有数据包丢掉</span><span>。</span>

<span>![15_83.png.jpg](images/15_83.png.jpg)</span><span>删除刚刚插入的规则</span><span>。</span><span>注意要删除一条规则时，必须和插入的规则一致，也就是说，两条</span><span>iptables</span><span>命令，除了</span><span>-I</span> <span>和</span><span>-D</span><span>不一样外，其他地方都一样</span><span>。</span>

<span>![15_165.png.jpg](images/15_165.png.jpg)</span>

<span>上例表示把来自</span><span>10.0.2.36</span> <span>并且是</span><span>tcp</span><span>协议到本机的</span><span>80</span><span>端口的数据包丢掉</span><span>。</span><span>这里要说的是，</span><span>--dport/--sport</span> <span>必须要和</span><span>-p</span><span>选项一起使用，否则会出错</span><span>。</span>

<span>![15_166.png.jpg](images/15_166.png.jpg)</span>

<span>把发送到</span><span>10.0.2.34</span><span>的</span><span>22</span><span>端口的数据包丢掉</span><span>。</span><span>下面做一个小试验：</span>

<span>![15_167.png.jpg](images/15_167.png.jpg)</span>

<span>一开始用本机</span><span>ping 10.0.2.34</span><span>是通的，然后使用</span><span>iptables</span><span>增加一条规则，使到</span><span>10.0.2.34</span><span>的</span><span>icmp</span><span>包丢掉，再</span><span>ping 10.0.2.34</span><span>则不通了</span><span>。</span><span>此时用</span><span>’iptables –nvL’</span><span>查看</span><span>iptalbes</span><span>规则</span><span>。</span>

<span>![15_168.png.jpg](images/15_168.png.jpg)</span><span>会有一条这样的记录，看</span><span>pkts</span><span>那列显示</span><span>4</span><span>个数据包，因为我们</span><span>ping</span> <span>的时候给</span><span>10.0.2.34</span><span>发送了</span><span>4</span><span>个数据包，第二列表示这</span><span>4</span><span>个数据包一共有多大（</span><span>336bytes</span><span>）</span><span>。</span><span>此时使用</span><span>’iptables -Z'</span> <span>清零</span><span>。</span>

<span>![15_169.png.jpg](images/15_169.png.jpg)</span>

<span>现在你明白</span><span>’iptables -Z’</span><span>的意义了吧</span><span>。</span><span>至于</span><span>FORWORD</span><span>链的应用笔者几乎没有用到过，所以不再举例</span><span>。</span><span>再总结一下各个选项的作用：</span>

<span>-A/-D</span> <span>：增加删除一条规则；</span>

<span>-I</span> <span>：插入一条规则，其实跟</span><span>-A</span><span>的效果一样；</span>

<span>-p</span> <span>：指定协议，可以是</span><span>tcp</span><span>，</span><span>udp</span><span>或者</span><span>icmp</span><span>；</span>

<span>--dport</span> <span>：跟</span><span>-p</span><span>一起使用，指定目标端口；</span>

<span>--sport</span> <span>：跟</span><span>-p</span><span>一起使用，指定源端口；</span>

<span>-s</span> <span>：指定源</span><span>IP</span><span>（可以是一个</span><span>ip</span><span>段）；</span>

<span>-d</span> <span>：指定目的</span><span>IP</span><span>（可以是一个</span><span>ip</span><span>段）；</span>

<span>-j</span> <span>：后跟动作，其中</span><span>ACCEPT</span><span>表示允许包，</span><span>DROP</span><span>表示丢掉包，</span><span>REJECT</span><span>表示拒绝包；</span>

<span>-i</span> <span>：指定网卡（不常用，但有时候能用到）；</span>

<span>![15_170.png.jpg](images/15_170.png.jpg)</span>

<span>上例中表示，把来自</span><span>10.0.2.0/24</span><span>这个网段的并且作用在</span><span>eth0</span><span>上的包放行</span><span>。</span><span>有时候你的服务器上</span><span>iptables</span><span>过多了，想删除某一条规则时，又不容易掌握当时创建时的规则</span><span>。</span><span>其实有一种比较简单的方法：</span>

<span>![15_171.png.jpg](images/15_171.png.jpg)</span>

<span>查看结果如下：</span>

<span>![15_172.png.jpg](images/15_172.png.jpg)</span>

<span>删除某一个规则的方法是：</span>

<span>![15_173.png.jpg](images/15_173.png.jpg)</span>

<span>-D</span> <span>后跟链名，然后是规则</span><span>num</span><span>，这个</span><span>num</span><span>就是查看</span><span>iptables</span><span>规则时第一列的值</span><span>。</span>

<span>iptables</span><span>还有一个选项经常用到，</span><span>-P</span><span>（大写）选项，表示预设策略</span><span>。</span><span>用法如下：</span>

<span>![15_174.png.jpg](images/15_174.png.jpg)</span>

<span>-P</span><span>后面跟链名，策略内容或者为</span><span>DROP</span><span>或者为</span><span>ACCEPT</span><span>，默认是</span><span>ACCEPT。</span><span>注意：如果你在连接远程服务器，千万不要随便敲这个命令，因为一旦你敲完回车你就会断掉</span><span>。</span>

<span>![15_175.png.jpg](images/15_175.png.jpg)</span>

<span>看到上图中红框标出的部分了吧，现在所有进来的数据包全部</span><span>DROP</span><span>了</span><span>。</span><span>这个策略一旦设定后，只能使用</span><span>iptables -P ACCEPT</span><span>才能恢复成原始状态，而不能使用</span><span>-F</span><span>参数</span><span>。</span><span>下面笔者针对一个小需求讲述一下这个</span><span>iptables</span><span>规则如何设定</span><span>。</span>

<span>需求：只针对</span><span>filter</span><span>表，预设策略</span><span>INPUT</span><span>链</span><span>DROP</span><span>，其他两个链</span><span>ACCEPT</span><span>，然后针对</span><span>10.0.2.0/24</span><span>开通</span><span>22</span><span>端口，对所有网段开放</span><span>80</span><span>端口，对所有网段开放</span><span>21</span><span>端口</span><span>。</span>

<span>这个需求不算复杂，但是因为有多条规则，所以最好写成脚本的形式</span><span>。</span>

<span>![15_176.png.jpg](images/15_176.png.jpg)</span>

<span>完成脚本的编写后，直接运行</span> <span>‘sh /usr/local/sbin/iptables.sh ’</span> <span>即可</span><span>。</span><span>如果想开机启动时初始化防火墙规则，则需要在</span><span>/etc/rc.d/rc.local</span> <span>中添加一行</span> <span>‘sh /usr/local/sbin/iptables.sh’ 。</span>

<span>关于</span><span>icmp</span><span>的包有一个比较常见的应用</span><span>。</span>

<span>![15_177.png.jpg](images/15_177.png.jpg)</span>

<span>--icmp-type</span> <span>这个选项是要跟</span><span>-p icmp</span> <span>一起使用的，后面指定类型编号</span><span>。</span><span>这个</span><span>8</span><span>指的是能在本机</span><span>ping</span><span>通其他机器，而其他机器不能</span><span>ping</span><span>通本机</span><span>。</span><span>这个有必要记一下</span><span>。</span>

<span>**C. nat**</span><span>**表的应用**</span>

<span>其实，</span><span>linux</span><span>的</span><span>iptables</span><span>功能是十分强大的，笔者曾经的一个老师这样形容</span><span>linux</span><span>的网络功能：只有想不到没有做不到！也就是说只要你能够想到的关于网络的应用，</span><span>linux</span><span>都能帮你实现</span><span>。</span><span>在日常生活中相信你接触过路由器吧，它的功能就是分享上网</span><span>。</span><span>本来一根网线过来（其实只有一个公网</span><span>IP</span><span>），通过路由器后，路由器分配了一个网段（私网</span><span>IP</span><span>），这样连接路由器的多台</span><span>pc</span><span>都能连接</span><span>intnet</span><span>而远端的设备认为你的</span><span>IP</span><span>就是那个连接路由器的公网</span><span>IP。</span><span>这个路由器的功能其实就是由</span><span>linux</span><span>的</span><span>iptables</span><span>实现的，而</span><span>iptables</span><span>又是通过</span><span>nat</span><span>表作用而实现的这个功能</span><span>。</span>

<span>至于具体的原理以及过程，笔者不想阐述，请查看相关资料</span><span>。</span><span>笔者在这里只举一个例子来说明</span><span>iptables</span><span>如何实现的这个功能</span><span>。</span><span>假设你的机器上有两块网卡</span><span>eth0</span><span>和</span><span>eth1</span><span>，其中</span><span>eth0</span><span>的</span><span>IP</span><span>为</span><span>10.0.2.68</span> <span>，</span><span>eth1</span><span>的</span><span>IP</span><span>为</span><span>192.168.1.1 。eth0</span><span>连接了</span><span>intnet</span> <span>但</span><span>eth1</span><span>没有连接，现在有另一台机器（</span><span>192.168.1.2</span><span>）和</span><span>eth1</span><span>是互通的，那么如何设置也能够让连接</span><span>eth1</span><span>的这台机器能够连接</span><span>intnet</span><span>（即能和</span><span>10.0.2.68</span><span>互通）</span><span>?</span>

<span>![15_178.png.jpg](images/15_178.png.jpg)</span>

<span>其实就是这样简单的两个命令就能实现上面的需求</span><span>。</span><span>第一个命令涉及到了内核参数相关的配置文件，它的目的是为了打开路由转发功能，否则无法实现我们的应用</span><span>。</span><span>第二个命令则是</span><span>iptables</span><span>对</span><span>nat</span><span>表做了一个</span><span>IP</span><span>转发的操作，</span><span>-o</span> <span>选项后跟设备名，表示出口的网卡，</span><span>MASQUERADE</span><span>表示伪装的意思</span><span>。</span>

<span>关于</span><span>nat</span><span>表，笔者不想讲太多内容，你只要学会这个路由转发即可</span><span>。</span><span>其他的东西交给网络工程师去学习吧，毕竟你将来可是要做</span><span>linux</span><span>系统工程师的</span><span>。</span>

<span>**D.** </span><span>**保存以及备份**</span><span>**iptalbes**</span><span>**规则**</span>

<span>也许你不知道，咱们设定的防火墙规则只是保存在内存中，并没有保存到某一个文件中，也就说当系统重启后以前设定的规则就没有了，所以设定好规则后要先保存一下</span><span>。</span>

<span>![15_179.png.jpg](images/15_179.png.jpg)</span>

<span>它会提示你把规则保存在了</span><span>/etc/sysconfig/iptables</span><span>文件内</span><span>。</span><span>其实，这个文件就是</span><span>iptables</span><span>的配置文件了，你不妨查看一下它</span><span>。</span>

<span>![15_180.png.jpg](images/15_180.png.jpg)</span>

<span>红线部分就是咱们刚才设定那条规则！有时可能因为我们设置防火墙规则有误导致服务器出问题，这时候不妨先备份一下这个配置文件，然后停止防火墙服务</span><span>。</span>

<span>![15_181.png.jpg](images/15_181.png.jpg)</span>

<span>这样防火墙就失效了，但是一旦你重新设定规则后（哪怕只有一条），防火墙又开始工作了</span><span>。</span>

<span>![15_182.png.jpg](images/15_182.png.jpg)</span>

<span>我还可以使用</span><span>iptables-save >filename</span> <span>这条命令来保存一个防火墙规则，这样就可以起到备份的作用了</span><span>。</span><span>要想恢复这个规则使用下面这个命令即可</span><span>。</span>

<span>![15_183.png.jpg](images/15_183.png.jpg)</span>

<span>【</span><span>**linux**</span><span>**系统的任务计划**</span><span>】</span>

<span>这部分内容太重要了，其实大部分系统管理工作都是通过定期自动执行某一个脚本来完成的，那么如何定期执行某一个脚本呢？这就要借助</span><span>linux</span><span>的</span><span>cron</span><span>功能了</span><span>。</span>

<span>![15_184.png.jpg](images/15_184.png.jpg)</span>

<span>关于</span><span>cron</span><span>任务计划功能的操作都是通过</span><span>crontab</span><span>这个命令来完成的</span><span>。</span><span>其中常用的选项有：</span>

<span>-u</span> <span>：指定某个用户，不加</span><span>-u</span><span>选项则为当前用户；</span>

<span>-e</span> <span>：制定计划任务；</span>

<span>-l</span> <span>：列出计划任务；</span>

<span>-r</span> <span>：删除计划任务</span><span>。</span>

<span>![15_185.png.jpg](images/15_185.png.jpg)</span>

<span>使用</span><span>crontab -e</span> <span>来制定计划任务，上面的例子表示在</span><span>05</span><span>月</span><span>26</span><span>日（这天必须是周四）的</span><span>10</span><span>点</span><span>01</span><span>分执行</span><span>’ echo "ok" >/root/cron.log’</span><span>这样的任务</span><span>。</span>

<span>Cron</span><span>的格式是这样的，每一行代表一个任务计划，总共分成两部分，</span><span>前面部分为时间，后面部分要执行的命令</span><span>。</span><span>后面的命令不用多讲，至于前面的时间是有讲究的，这个时间共分为</span><span>5</span><span>段，用空格隔开（可以是多个空格），</span><span>第一段表示分钟</span><span>(0-59)</span><span>，第二段表示小时</span><span>(0-23)</span><span>，第三段表示日</span><span>(1-31)</span><span>，第四段表示月</span><span>(1-12)</span><span>，第五段表示周</span><span>(0-7,0</span><span>或者</span><span>7</span><span>都可以表示为周日</span><span>)。</span><span>从左至右依次是：分，时，日，月，周</span><span>（一定要牢记）！</span>

<span>crontab -e</span> <span>实际上是打开了</span><span>/var/spool/cron/username</span> <span>（如果是</span><span>root</span><span>则打开的是</span><span>/var/spool/cron/root</span><span>）这个文件</span><span>。</span><span>使用的是</span><span>vim</span><span>编辑器，所以要保存的话则在命令模式下输入</span><span>:wq</span><span>即可</span><span>。</span><span>但是，你千万不要直接去编辑那个文件，因为可能会出错，所以一定要使用</span><span>crontab -e</span><span>来编辑</span><span>。</span><span>查看已经设定的任务计划使用</span><span>crontab -l</span>

<span>![15_186.png.jpg](images/15_186.png.jpg)</span>

<span>删除计划任务要用</span><span>crontab -r</span>

<span>![15_187.png.jpg](images/15_187.png.jpg)</span>

<span>下面笔者给你出一些练习题，帮助你熟悉这个</span><span>cron</span><span>的应用</span><span>。</span>

<span>1\.</span> <span>每天凌晨</span><span>1</span><span>点</span><span>20</span><span>分清除</span><span>/var/log/slow.log</span><span>这个文件；</span>

<span>2\.</span> <span>每周日</span><span>3</span><span>点执行</span><span>’/bin/sh /usr/local/sbin/backup.sh’</span><span>；</span>

<span>3\.</span> <span>每月</span><span>14</span><span>号</span><span>4</span><span>点</span><span>10</span><span>分执行</span><span>’/bin/sh /usr/local/sbin/backup_month.sh’</span><span>；</span>

<span>4\.</span> <span>每隔</span><span>8</span><span>小时执行</span><span>’ntpdate time.windows.com’</span><span>；</span>

<span>5\.</span> <span>每天的</span><span>1</span><span>点，</span><span>12</span><span>点，</span><span>18</span><span>点执行</span><span>’/bin/sh /usr/local/sbin/test.sh’</span><span>；</span>

<span>6\.</span> <span>每天的</span><span>9</span><span>点到</span><span>18</span><span>点执行</span><span>’/bin/sh /usr/local/sbin/test2.sh’</span><span>；</span>

<span>答案：</span>

<span>1\. 20 1 * * * echo “”>/var/log/slow.log</span>

<span>2\. 0 30 * * 0 /bin/sh /usr/local/sbin/backup.sh</span>

<span>3\. 10 04 14 * * /bin/sh /usr/local/sbin/backup_month.sh</span>

<span>4\. 0 */8 * * * ntpdate time.windows.com</span>

<span>5\. 0 1,12,18 * * /bin/sh /usr/local/sbin/test.sh</span>

<span>6\. 0 9-18 * * * /bin/sh /usr/local/sbin/test2.sh</span>

<span>Cron</span><span>的这部分内容并不难，你只要会了这</span><span>6</span><span>道练习题，你就算掌握它了</span><span>。</span><span>这里要简单说一下，每隔</span><span>8</span><span>小时，就是用全部小时（</span><span>0-23</span><span>）去除以</span><span>8</span><span>，你仔细想一下结果，其实算出来应该是</span><span>0,8,16</span><span>三个数</span><span>。</span><span>当遇到多个数（分钟</span><span>、</span><span>小时</span><span>、</span><span>月</span><span>、</span><span>周）例如第</span><span>5</span><span>题，则需要用逗号隔开</span><span>。</span><span>而时间段是可以用</span><span>’-‘</span><span>的方式表示的</span><span>。</span><span>等设置好了所有的计划任务后需要查看一下</span><span>crond</span><span>服务是否启动，如果没有启动，需要启动它</span><span>。</span>

<span>![15_188.png.jpg](images/15_188.png.jpg)</span>

<span>如何启动稍后会做介绍</span><span>。</span><span>除了用户自定义的计划任务外，其实系统本身也有计划任务的</span><span>。</span>

<span>![15_189.png.jpg](images/15_189.png.jpg)</span>

<span>系统会安装这个配置文件中的计划去执行内定的任务</span><span>。</span>

<span>【</span><span>**linux**</span><span>**的系统服务管理**</span><span>】</span>

<span>如果你对</span><span>windows</span><span>非常熟悉的话，相信你肯定配置过开机启动的服务，有些服务我们日常用不到则要把它停掉，一来可以节省资源，二来可以减少安全隐患</span><span>。</span><span>在</span><span>linux</span><span>上同样也有相关的工具来管理系统的服务</span><span>。</span>

<span>**1\. ntsysv**</span>

<span>用来配置哪些服务开启或者关闭，有点想图形界面，不过是使用键盘来控制的</span><span>。</span><span>如果没有这个命令请使用</span> <span>yum install -y ntsysv</span> <span>安装它</span><span>。</span>

<span>![15_190.png.jpg](images/15_190.png.jpg)</span>

<span>敲完这个命令后则显示出如上图中的画面</span><span>。</span><span>在屏幕的最上面有</span><span>’Red Hat’</span><span>等字样，这是在告诉我们这个工具是由</span><span>Red Hat</span><span>公司开发的</span><span>。</span><span>按键盘的上下方向键可以调节红色光标，按空格可以选择开启或者不开启，如果前面的中括号内显示有</span><span>’*’</span> <span>则表示开启否则不开启</span><span>。</span><span>通过这个工具也可以看到目前系统中所有的服务</span><span>。</span><span>建议除</span><span>’crond, iptables, network, sshd, syslog, irqbalance, sendmail, microcode_ctl’</span> <span>外其他服务全部停掉</span><span>。</span><span>选择好后，按</span><span>’tab’</span><span>键选择</span><span>ok</span><span>然后回车</span><span>。</span><span>需要重启机器才能生效</span><span>。</span>

<span>**2\. chkconfig**</span>

<span>Linux</span><span>系统所有的预设服务可以查看</span><span>/etc/init.d/</span><span>目录得到</span>

<span>![15_191.png.jpg](images/15_191.png.jpg)</span>

<span>其实这就是系统所有的预设服务了</span><span>。</span><span>为什么这样讲，因为系统预设服务都是可以通过这样的命令实现</span> <span>‘service</span> <span>服务名</span> <span>start|stop|restart’</span> <span>，这里的服务名就是</span><span>/etc/init.d/</span><span>目录下的这些文件了</span><span>。</span><span>除了可以使用</span><span>’service crond start ‘</span><span>启动</span><span>crond</span><span>外，还可以使用</span><span>/etc/init.d/crond start</span> <span>来启动</span><span>。</span>

<span>![15_192.png.jpg](images/15_192.png.jpg)</span>

<span>如上图，这两个命令出来的结果是一样的</span><span>。</span>

<span>![15_193.png.jpg](images/15_193.png.jpg)</span>

<span>再看看这个</span><span>chkconfig</span><span>命令，它不仅可以列出来所有的服务，还可以详细到每个级别</span><span>。</span><span>这里的级别（</span><span>0,1,2,3,4,5,6</span><span>）就是</span><span>inittab</span><span>里面介绍的那几个启动级别了</span><span>。</span>

<span>![15_194.png.jpg](images/15_194.png.jpg)</span>

<span>这样还可以查看某一个服务的启动情况</span><span>。</span>

<span>![15_195.png.jpg](images/15_195.png.jpg)</span>

<span>用</span><span>--level</span> <span>指定级别，后面是服务名，然后是</span><span>off</span><span>或者</span><span>on</span><span>，</span><span>--level</span><span>后还可以跟多个级别</span><span>。</span>

<span>![15_196.png.jpg](images/15_196.png.jpg)</span>

<span>另外还可以省略级别，默认是针对</span><span>2,3,4,5</span><span>级别操作</span><span>。</span>

<span>![15_197.png.jpg](images/15_197.png.jpg)</span>

<span>另外这个</span><span>chkconfig</span> <span>还有一个功能就是可以把某个服务加入到系统服务，即可以使用</span><span>service</span> <span>服务名</span> <span>start</span> <span>这样的形式，并且可以在</span><span>chkconfig --list</span> <span>中查找到</span><span>。</span><span>当然也能删除掉</span><span>。</span>

<span>![15_198.png.jpg](images/15_198.png.jpg)</span>

<span>这个功能常用在把自定义的启动脚本加入到系统服务当中</span><span>。</span><span>关于系统服务就讲这些内容，其实还有很多内容笔者没有介绍，道理很简单，一来讲多了你不能消化二来讲多了你也用不上</span><span>。</span>

<span>【</span><span>**linux**</span><span>**中的数据备份**</span><span>】</span>

<span>数据备份，不用说太多吧，毫无疑问很重要</span><span>。</span><span>笔者就曾经有过一次非常痛苦的经历，备份策略没有做好，结果磁盘坏掉数据丢失，简直是撕心裂肺的痛呀</span><span>。</span><span>还好数据重要性不是特别高，即使是不高也是丢失了数据，这是作为系统管理员最不应该出现的事故</span><span>。</span><span>所以，在你以后的系统维护工作中，一定要把数据备份当回事，认真对待</span><span>。</span><span>在</span><span>linux</span><span>上作为数据备份的工具很多，但笔者就只用一种那就是</span><span>rsync</span> <span>从字面上的意思你可以理解为</span><span>remote sync</span> <span>（远程同步）这样可以让你理解的更深刻一些</span><span>。Rsync</span><span>不仅可以远程同步数据（类似于</span><span>scp</span><span>），当然还可以本地同步数据（类似于</span><span>cp</span><span>），但不同于</span><span>cp</span><span>或</span><span>scp</span><span>的一点是，</span><span>rsync</span><span>不像</span><span>cp/scp</span><span>一样会覆盖以前的数据（如果数据已经存在），它会先判断已经存在的数据和新数据有什么不同，只有不同时才会把不同的部分覆盖掉</span><span>。</span><span>如果你的</span><span>linux</span><span>上下面看例子吧</span><span>。</span><span>（如果没有</span><span>rsync</span><span>命令请使用</span><span>yum install -y rsync</span><span>安装）</span>

<span>![15_199.png.jpg](images/15_199.png.jpg)</span>

<span>上面例子表示把当前目录下的</span><span>123</span><span>同步到</span><span>/tmp/</span><span>目录下，并且同样也命名为</span><span>123。</span><span>如果是远程拷贝的话就是这样的形式了</span> <span>IP:path</span> <span>（如：</span><span>10.0.2.34:/root/</span><span>）</span>

<span>![15_200.png.jpg](images/15_200.png.jpg)</span>

<span>当建立连接后，是需要输入密码的</span><span>。</span><span>如果手动去执行这些操作还好，但是如果是写在脚本中怎么办？这就涉及到添加信任关系了，该部分内容稍后会详细介绍</span><span>。</span>

<span>**1\. rsync**</span><span>**的命令格式**</span>

<span>rsync [OPTION]... SRC DEST</span>

<span>rsync [OPTION]... SRC [USER@]HOST:DEST</span>

<span>rsync [OPTION]... [USER@]HOST:SRC DEST</span>

<span>rsync [OPTION]... [USER@]HOST::SRC DEST</span>

<span>rsync [OPTION]... SRC [USER@]HOST::DEST</span>

<span>笔者在一开始举的两个例子，第一个例子即为第一种格式，第二个例子即为第二种格式，但不同的是，笔者并没有加</span><span>user@host</span> <span>如果不加默认指的是</span><span>root 。</span><span>第三种格式是从远程目录同步数据到本地</span><span>。</span><span>第四种以及第五种格式使用了两个冒号，这种方式和前面的方式的不同在于验证方式不同，稍后详细介绍</span><span>。</span>

<span>**2\. rsync**</span><span>**常用选项**</span>

<span>-a</span><span>：归档模式，表示以递归方式传输文件，并保持所有属性，等同于</span><span>-</span><span>rlptgoD</span> <span>，</span><span>-a</span><span>选项后面可以跟一个</span> <span>--no-OPTION</span> <span>这个表示关闭</span><span>-rlptgoD</span><span>中的某一个例如</span> <span>-a --no-l</span> <span>等同于</span><span>-rptgoD</span>

<span>-r</span> <span>：对子目录以递归模式处理，主要是针对目录来说的，如果单独传一个文件不需要加</span><span>-r</span><span>，但是传输的是目录必须加</span><span>-r</span><span>选项</span>

<span>-v</span> <span>：打印一些信息出来，比如速率，文件数量等</span>

<span>-l</span> <span>：保留软链结</span>

<span>-L</span> <span>：向对待常规文件一样处理软链结，如果是</span><span>SRC</span><span>中有软连接文件，则加上该选项后将会把软连接指向的目标文件拷贝到</span><span>DST</span>

<span>-p</span> <span>：保持文件权限</span>

<span>-o</span> <span>：保持文件属主信息</span>

<span>-g</span> <span>：保持文件属组信息</span>

<span>-D</span> <span>：保持设备文件信息</span>

<span>-t</span> <span>：保持文件时间信息</span>

<span>--delete</span> <span>：删除那些</span><span>DST</span><span>中</span><span>SRC</span><span>没有的文件</span>

<span>--exclude=PATTERN</span><span>：指定排除不需要传输的文件，等号后面跟文件名，可以是万用字符模式（如</span><span>*.txt</span><span>）</span>

<span>-u</span> <span>：加上这个选项后将会把</span><span>DST</span><span>中比</span><span>SRC</span><span>还新的文件排除掉，不会覆盖</span>

<span>下面笔者将会针对这些选项做一些列小实验：</span>

<span>1</span><span>）</span><span>建立目录以及文件</span>

<span>![15_201.png.jpg](images/15_201.png.jpg)</span>

<span>笔者建立这些文件的目的就是为做试验做一些准备工作</span><span>。</span>

<span>2</span><span>）使用</span><span>-a</span><span>选项</span>

<span>![15_202.png.jpg](images/15_202.png.jpg)</span>

<span>这里有一个问题，就是本来想把</span><span>test1</span><span>目录直接拷贝成</span><span>test2</span><span>目录，可结果</span><span>rsync</span><span>却新建了</span><span>test2</span><span>目录然后把</span><span>test1</span><span>放到</span><span>test2</span><span>当中</span><span>。</span><span>为了避免这样的情况发生，可以这样做：</span>

<span>![15_203.png.jpg](images/15_203.png.jpg)</span>

<span>加一个斜杠就好了，所以笔者建议你</span><span>在使用</span><span>rsync</span><span>备份目录时要养成加斜杠的习惯</span><span>。</span><span>在上面讲了</span><span>-a</span><span>选项等同于</span><span>-</span> <span>rlptgoD</span><span>，而且</span><span>-a</span><span>还可以和</span><span>--no-OPTION</span><span>一并使用</span><span>。</span>

<span>![15_204.png.jpg](images/15_204.png.jpg)</span>

<span>笔者加上</span><span>-v</span><span>选项来获得更多的信息，上例中因为没有使用</span><span>-r</span><span>选项导致只能拷贝目录但不能拷贝目录下面的内容（英文翻译过来就是</span><span>“</span><span>忽略了目录</span><span>test1/.”</span><span>，其中</span><span>test1/.</span><span>指的就是</span><span>test1</span><span>目录内部的所有文件），所以虽然创建了</span><span>test2</span><span>目录，但是</span><span>test2</span><span>目录为空</span><span>。</span><span>下面再看看那个</span><span>-l</span><span>选项的作用</span><span>。</span>

<span>![15_205.png.jpg](images/15_205.png.jpg)</span>

<span>使用</span><span>-v</span><span>选项看来就是方便呀，上例告诉我们跳过了非普通文件</span><span>1.sh</span><span>，其实</span><span>1.sh</span><span>是一个软连接文件，如果不使用</span><span>-l</span><span>选项则不会理会软连接文件的</span><span>。</span>

<span>![15_206.png.jpg](images/15_206.png.jpg)</span>

<span>果真</span><span>test2</span><span>目录当中没有那个</span><span>1.sh</span><span>的影子</span><span>。</span><span>当然加上</span><span>-l</span><span>选项则会把软连接文件给拷贝过去，但是软连接的目标文件却没有拷贝过去，有时候咱们指向拷贝软连接文件所指向的目标文件，那这时候该怎么办呢？</span>

<span>3</span><span>）使用</span><span>-L</span><span>选项</span>

<span>![15_207.png.jpg](images/15_207.png.jpg)</span>

<span>一个</span><span>-L</span><span>就可以把</span><span>SRC</span><span>中软连接的目标文件给拷贝到</span><span>DST</span>

<span>4</span><span>）</span><span>使用</span><span>-u</span><span>选项</span>

<span>首先查看一下</span><span>test1/1</span> <span>和</span> <span>test2/1</span><span>的访问时间（肯定是一样的），然后使用</span><span>touch</span><span>修改一下</span><span>test2/1</span><span>的访问时间（此时</span><span>test2/1</span><span>要比</span><span>test1/1</span><span>的访问时间晚了一些），如果不加</span><span>-u</span><span>选项的话，会把</span><span>test2/1</span><span>的访问时间变成和</span><span>test1/1</span><span>的访问时间一样</span><span>。</span><span>这样讲也许你会迷糊，不妨看一看</span><span>。</span>

<span>![15_208.png.jpg](images/15_208.png.jpg)</span>

<span>看到了吧，本来</span><span>test2/1</span><span>的访问时间已经不同于</span><span>test1/1</span><span>的访问时间了，但是同步后访问时间又一致了</span><span>。</span>

<span>![15_209.png.jpg](images/15_209.png.jpg)</span>

<span>现在你明白</span><span>-u</span><span>选项的妙用了吧</span><span>。</span>

<span>5</span><span>）使用</span><span>--delete</span><span>选项</span>

<span>![15_210.png.jpg](images/15_210.png.jpg)</span>

<span>如果不使用</span><span>--delete</span><span>选项当</span><span>SRC</span><span>有文件删除时，</span><span>DST</span><span>是不会删除的，只有加上</span><span>--delete</span><span>选项后才能删除掉</span><span>。</span><span>还有一种情况就是如果在</span><span>DST</span><span>增加文件了，而</span><span>SRC</span><span>当中没有这些文件，同步时加上</span><span>--delete</span><span>选项后同样会删除新增的文件</span><span>。</span>

<span>![15_211.png.jpg](images/15_211.png.jpg)</span>

<span>6</span><span>）使用</span><span>--exclude</span> <span>选项</span>

<span>![15_212.png.jpg](images/15_212.png.jpg)</span>

<span>另外还可以使用万用字符</span><span>*</span><span>匹配</span>

<span>![15_213.png.jpg](images/15_213.png.jpg)</span>

<span>最后简单总结一下，平时你使用</span><span>rsync</span><span>同步数据的时候，使用</span><span>-a</span><span>选项基本上就可以达到我们想要的效果了，只是有时候会有个别的需求，会用到</span><span>-a --no-OPTION, -u, -L, --delete, --exclude</span><span>这些选项，但是笔者要求你把上面这些全部掌握，毕竟这才几个而已，大部分选项笔者都没有介绍</span><span>。</span><span>如果在以后的工作中遇到特殊需求了，就去查一下</span><span>rsync</span><span>的</span><span>man</span><span>文档吧</span><span>。</span>

<span>**3\. rsync** </span><span>**应用实例**</span>

<span>**1**</span><span>**）通过**</span><span>**ssh**</span><span>**的方式**</span>

<span>最上面介绍的</span><span>5</span><span>种方式当中，第二</span><span>、</span><span>第三（</span><span>1</span><span>个冒号）就属于通过</span><span>ssh</span><span>的方式，这种方式其实就是让用户去登录到远程机器，然后执行</span><span>rsync</span><span>的任务</span><span>。</span>

<span>![15_214.png.jpg](images/15_214.png.jpg)</span>

<span>这种方式就是前面介绍的第二种方式了，是通过</span><span>ssh</span><span>拷贝的数据，是要输入</span><span>10.0.2.69</span><span>那台机器</span><span>root</span><span>的密码的</span><span>。</span>

<span>![15_215.png.jpg](images/15_215.png.jpg)</span>

<span>这个则为第三种方式</span><span>。</span><span>这两种方式如果写到脚本里，备份起来就有麻烦了，因为要输入密码，脚本本来就是自动的，不可能做到的</span><span>。</span><span>但是不代表没有解决办法</span><span>。</span><span>那就是通过密钥验证，密钥不设立密码就</span><span>ok</span><span>了</span><span>。</span><span>还记得在前面笔者曾经介绍过通过密钥登录远程主机吗，下面要讲的内容就是那些东西了</span><span>。</span>

<span>先提前说一下基本的主机信息：</span> <span>10.0.2.68</span> <span>（主机名</span><span>Aming-1</span><span>）和</span><span>10.0.2.69</span><span>（主机名</span><span>Aming</span><span>）需要从</span><span>Aming-1</span><span>上拷贝数据到</span><span>Aming</span><span>上</span><span>。</span>

<span>A.</span> <span>首先确认一下</span><span>Aming-1</span><span>上是否有这个文件</span> <span>/root/.ssh/id_rsa.pub</span>

<span>![15_216.png.jpg](images/15_216.png.jpg)</span>

<span>如果没有安装以下的方法生成：</span>

<span>![15_217.png.jpg](images/15_217.png.jpg)</span>

<span>在这个过程中会有一些交互的过程，因为笔者的</span><span>/root/.ssh/id_rsa</span><span>已经存在，所以会问是否覆盖，笔者选择覆盖，然后会提示要输入这个密钥的密码，出于安全考虑应该定义个密码，但是我们的目的就是为了自动化同步数据，所以这里不输入任何密码，直接按回车，即密码为空</span><span>。</span><span>最后则生成了私钥</span><span>(/root/.ssh/id_rsa)</span><span>和公钥文件</span><span>(/root/.ssh/id_rsa.pub)</span>

<span>B.</span> <span>把公钥文件的内容拷贝到目标机器上</span>

<span>![15_218.png.jpg](images/15_218.png.jpg)</span>

<span>复制主机</span><span>Aming-1</span><span>的</span><span>/root/.ssh/id_rsa.pub</span><span>文件内容，并粘贴到主机</span><span>Aming</span><span>的</span><span>/root/.ssh/authorized_keys</span><span>中</span>

<span>![15_219.png.jpg](images/15_219.png.jpg)</span>

<span>在这一步也许你会遇到</span><span>/root/.ssh</span><span>目录不存在的问题，可以手动创建，并修改目录权限为</span><span>700</span><span>也可以执行</span><span>ssh-keygen</span><span>命令生成这个目录</span><span>。</span><span>保存</span><span>/root/.ssh/authorized_keys</span><span>文件后，再到主机</span><span>Aming-1</span><span>上执行</span>

<span>![15_220.png.jpg](images/15_220.png.jpg)</span>

<span>你会发现，现在不用输入密码也可以登录主机</span><span>Aming</span><span>了</span><span>。</span><span>下面再从主机</span><span>Aming-1</span><span>上执行一下</span><span>rsync</span><span>命令试试吧</span><span>。</span>

<span>![15_221.png.jpg](images/15_221.png.jpg)</span>

<span>**2**</span><span>**）通过后台服务的方式**</span>

<span>这种方式可以理解成这样，在远程主机上建立一个</span><span>rsync</span><span>的服务器，在服务器上配置好</span><span>rsync</span><span>的各种应用，然后本机作为</span><span>rsync</span><span>的一个客户端去连接远程的</span><span>rsync</span><span>服务器</span><span>。</span><span>下面笔者就介绍一下，如何去配置一台</span><span>rsync</span><span>服务器</span><span>。</span>

<span>A.</span> <span>建立并配置</span><span>rsync</span><span>的配置文件</span> <span>/etc/rsyncd.conf</span>

<span>![15_222.png.jpg](images/15_222.png.jpg)</span>

<span>其中配置文件分为两部分全部配置部分和模块配置部分，全局部分就是几个参数而已，就像笔者的</span><span>rsyncd.conf</span><span>中</span><span>port, log file, pid file, address</span><span>这些都属于全局配置，而</span><span>[test]</span> <span>以下部分就是模块配置部分了</span><span>。</span><span>一个配置文件中可以有多个模块，模块名自定义，格式就像笔者的</span><span>rsyncd.conf</span><span>中的这样</span><span>。</span><span>其实模块中的一些参数例如</span><span>use chroot, max connections, udi, gid, auth users, secrets file</span><span>以及</span><span>hosts allow</span><span>都可以配置成全局的参数</span><span>。</span><span>当然笔者给出的参数并不是所有的，你可以通过</span><span>man rsyncd.conf</span> <span>获得更多信息</span><span>。</span>

<span>下面就简单解释一下这些参数的意义：</span>

<span>**port** </span><span>：指定在哪个端口启动</span><span>rsyncd</span><span>服务，默认是</span><span>873</span>

<span>**log file**</span><span>：指定日志文件</span>

<span>**pid file**</span><span>：指定</span><span>pid</span><span>文件，这个文件的作用涉及到服务的启动以及停止等进程管理操作</span>

<span>**address**</span><span>：指定启动</span><span>rsyncd</span><span>服务的</span><span>IP</span><span>，假如你的机器有多个</span><span>IP</span><span>，就可以指定其中一个启动</span><span>rsyncd</span><span>服务，默认是在全部</span><span>IP</span><span>上启动</span>

<span>**[test]** </span><span>：指定模块名，自定义</span>

<span>**path** </span><span>：指定数据存放的路径</span>

<span>**use chroot**</span><span>：</span><span>true|false</span> <span>默认是</span><span>true</span><span>，意思是在传输文件以前首先</span><span>chroot</span><span>到</span><span>path</span><span>参数所指定的目录下</span><span>。</span><span>这样做的原因是实现额外的安全防护，但是缺点是需要以</span><span>roots</span><span>权限，并且不能备份指向外部的符号连接所指向的目录文件</span><span>。</span><span>默认情况下</span><span>chroot</span><span>值为</span><span>true</span><span>，如果你的数据当中有软连接文件的话建议设置成</span><span>false。</span>

<span>**max connections**</span><span>：指定最大的连接数，默认是</span><span>0</span><span>即没有限制</span>

<span>**read only**</span><span>：</span><span>ture|false</span> <span>如果为</span><span>true</span><span>则不能上传到该模块指定的路径下</span>

<span>**list** </span><span>：指定当用户查询该服务器上的可用模块时，该模块是否被列出，设定为</span><span>true</span><span>则列出，</span><span>false</span><span>则隐藏</span>

<span>**uid/gid** </span><span>：指定传输文件时，以哪个用户</span><span>/</span><span>组的身份传输</span>

<span>**auth users**</span><span>：指定传输时要使用的用户名</span>

<span>**secrets file**</span><span>：指定密码文件，该参数连同上面的参数如果不指定则不使用密码验证</span>

<span>**hosts allow** </span><span>：指定被允许连接该模块的主机，可以是</span><span>IP</span><span>或者网段，如果是多个，之间用空格隔开</span>

<span>B.</span> <span>编辑</span><span>secrets file</span><span>，保存后要赋予</span><span>600</span><span>权限</span>

<span>![15_223.png.jpg](images/15_223.png.jpg)</span>

<span>C.</span> <span>启动</span><span>rsyncd</span><span>服务</span>

<span>![15_224.png.jpg](images/15_224.png.jpg)</span>

<span>启动后查看日志，看看是否有错误信息，然后再看下端口是否启动</span><span>。</span>

<span>![15_225.png.jpg](images/15_225.png.jpg)</span>

<span>如果想开机启动，请把</span><span>”rsync –daemon –confg=/etc/rsyncd.conf”</span> <span>写入到</span><span>/etc/rc.d/rc.local</span><span>文件</span><span>。</span>

<span>D.</span> <span>到另一台机器上测试</span>

<span>![15_226.png.jpg](images/15_226.png.jpg)</span>

<span>记得那个</span><span>use chroot</span><span>参数吗，如果设置为</span><span>true</span><span>，则</span><span>/root/test4/1.sh</span><span>不会被拷贝过来</span><span>。</span>

<span>![15_227.png.jpg](images/15_227.png.jpg)</span>

<span>修改</span><span>rsyncd.conf</span><span>文件，把</span><span>use chroot</span><span>改成</span><span>true</span><span>，不用重启服务即可生效</span><span>。</span>

<span>![15_228.png.jpg](images/15_228.png.jpg)</span>

<span>从上例中的详细信息中也可以看到，不能拷贝软连接的</span><span>。</span><span>所以请记住，如果涉及到软连接，请设置</span><span>use chroot=false 。</span><span>另外这种方式也是可以不用手动输入密码的，两种实现方式</span><span>。</span>

<span>第一种：指定密码文件</span>

<span>![15_229.png.jpg](images/15_229.png.jpg)</span>

<span>先编辑一个密码文件，并修改</span><span>600</span><span>权限</span><span>。</span>

<span>![15_230.png.jpg](images/15_230.png.jpg)</span>

<span>在同步时，指定密码文件即可</span><span>(--password-file=/etc/rsyncd.passwd)</span>

<span>第二种：在</span><span>rsync</span><span>服务器端不指定用户</span>

<span>![15_231.png.jpg](images/15_231.png.jpg)</span>

<span>把相关的参数都用</span><span>’#’</span><span>注释掉</span><span>。</span><span>然后再到客户端上测试</span><span>。</span>

<span>![15_232.png.jpg](images/15_232.png.jpg)</span>

<span>注意，这里不用再加</span><span>test@</span><span>这个用户了，默认是以</span><span>root</span><span>的身份拷贝的，现在已经不需要输入密码了</span><span>。</span>

<span>【</span><span>**linux**</span><span>**系统日志**</span><span>】</span>

<span>日志重要吗？必须的，没有日志你怎么知道你的系统状况？没有日志你如何排查一个</span><span>trouble</span><span>？日志记录了系统每天发生的各种各样的事情，你可以通过他来检查错误发生的原因，或者受到攻击时攻击者留下的痕迹</span><span>。</span><span>日志主要的功能有：审计和监测</span><span>。</span><span>他还可以实时的监测系统状态，监测和追踪侵入者等等</span><span>。</span>

<span>笔者常查看的日志文件为</span><span>/var/log/message.</span> <span>它是核心系统日志文件，包含了系统启动时的引导消息，以及系统运行时的其他状态消息</span><span>。IO</span> <span>错误</span><span>、</span><span>网络错误和其他系统错误都会记录到这个文件中</span><span>。</span><span>另外其他信息，比如某个人的身份切换为</span> <span>root</span><span>以及用户自定义安装的软件（</span><span>apache</span><span>）的日志也会在这里列出</span><span>。</span><span>通常，</span><span>/var/log/messages</span> <span>是在做故障诊断时首先要查看的文件</span><span>。</span><span>那你肯定会说了，这么多日志都记录到这个文件中，那如果服务器上有很多服务岂不是这个文件很快就会写的很大，没有错，但是系统有一个日志轮询的机制，每星期切换一个日志，变成</span><span>message.1, message.2,…messages.4</span> <span>连同</span><span>message</span><span>一共有</span><span>5</span><span>个这样的日志文件</span><span>。</span><span>这是通过</span><span>logrotate</span><span>工具的控制来实现的，它的配置文件是</span><span>/etc/logrotate.conf.</span> <span>如果没有特殊需求请不要修改这个配置文件</span><span>。</span>

<span>![15_233.png.jpg](images/15_233.png.jpg)</span>

<span>/var/log/message</span><span>是由</span><span>syslogd</span><span>这个守护进程产生的，如果停掉这个服务则系统不会产生</span><span>/var/log/message</span><span>，所以这个服务不要停</span><span>。Syslogd</span><span>服务的配置文件为</span><span>/etc/syslog.conf</span><span>这个文件定义了日志的级别，具体详细的东西笔者不再阐述，因为若没有特殊需求是不需要修改这个配置文件的，请使用</span><span>”man syslog.conf”</span> <span>获得更多关于它的信息</span><span>。</span>

<span>![15_234.png.jpg](images/15_234.png.jpg)</span>

<span>除了关注</span><span>/var/log/message</span><span>外，你还应该多关注一下</span><span>’dmesg’</span><span>这个命令，它可以显示系统的启动信息，如果你的某个硬件有问题（比如说网卡）用这个命令也是可以看到的</span><span>。</span>

<span>![15_235.png.jpg](images/15_235.png.jpg)</span>

<span>这一小节就介绍这么多，在结束之前，笔者给你一个小小的建议</span><span>。</span><span>以后在你日常的管理工总中要养成多看日志的习惯，尤其是一些应用软件的日志，比如</span><span>apache, mysql, php</span><span>等常用的软件，看它们的日志（错误日志）可以帮助你排查问题以及监控它们的运行状况是否良好</span><span>。</span>

<span>【</span><span>**xargs**</span><span>**与**</span><span>**-exec**</span><span>】</span>

<span>**1\. xargs**</span>

<span>在前面的例子中笔者曾经使用过这个命令，你是否有印象呢？现在就详细介绍一下它，平时笔者使用</span><span>xargs</span><span>还是比较多的，很方便</span><span>。</span>

<span>![15_236.png.jpg](images/15_236.png.jpg)</span>

<span>查看</span><span>xargs</span><span>的</span><span>man</span><span>文档，解释是这样的：</span><span>build and execute command lines from standard input.</span> <span>至于翻译成中文理解着有点困难</span><span>。</span><span>不妨笔者举个例子说明它的作用</span><span>。</span>

<span>![15_237.png.jpg](images/15_237.png.jpg)</span>

<span>它的作用就是把管道符前面的输出作为</span><span>xargs</span> <span>后面的命令的输入</span><span>。</span><span>它的好处在于可以把本来两步或者多步才能完成的任务简单一步就能完成</span><span>。xargs</span><span>常常和</span><span>find</span><span>命令一起使用，比如，查找当前目录创建时间大于</span><span>10</span><span>天的文件，然后再删除</span><span>。</span>

<span>![15_238.png.jpg](images/15_238.png.jpg)</span>

<span>这种应用是最为常见的，</span><span>xargs</span><span>后面的</span><span>rm</span> <span>也可以更选项，当是目录时，就需要</span><span>-r</span><span>选项了</span><span>。</span><span>在笔者看来</span><span>xargs</span><span>的这个功能不叫什么，它的另一个功能才叫神奇</span><span>。</span><span>现在我有一个这样的需求，查找当前目录下所有</span><span>.txt</span><span>的文件，然后把这些</span><span>.txt</span><span>的文件变成</span><span>.txt_bak 。</span><span>正常情况下，我们不得不写脚本去实现，但是使用</span><span>xargs</span><span>就一步</span><span>。</span>

<span>![15_239.png.jpg](images/15_239.png.jpg)</span>

<span>xargs -n1 –i{}</span> <span>类似</span><span>for</span><span>循环，</span><span>-n1</span><span>意思是一个一个对象的去处理，</span><span>-i{}</span> <span>把前面的对象使用</span><span>{}</span><span>取代，</span><span>mv {} {}_bak</span> <span>相当于</span> <span>mv 1.txt 1.txt_bak。</span><span>你刚开始接触这个命令时也许有点难以理解，多练习一下你就会熟悉了，笔者建议你记住这个应用，很实用</span><span>。</span>

<span>**2\. -exec**</span>

<span>使用</span><span>find</span><span>命令时，经常使用一个选项就是这个</span><span>-exec</span><span>了，可以达到和</span><span>xargs</span><span>同样的效果</span><span>。</span><span>比如，查找当前目录创建时间大于</span><span>10</span><span>天的文件并删除</span><span>。</span>

<span>![15_240.png.jpg](images/15_240.png.jpg)</span>

<span>这个命令中也是把</span><span>{}</span><span>作为前面</span><span>find</span><span>出来的文件的替代符，后面的</span><span>”\”</span><span>为</span><span>”;”</span><span>的脱意符，不然</span><span>shell</span><span>会把分号作为该行命令的结尾</span><span>。</span><span>这个</span><span>-exec</span><span>有时候也挺实用的</span><span>。</span>

<span>![15_241.png.jpg](images/15_241.png.jpg)</span>

<span>用</span><span>-exec</span><span>同样可以实现前面那个复杂的需求</span><span>。</span>

<span>【</span><span>**screen**</span><span>**工具介绍**</span><span>】</span>

<span>有时候，也许你会有这样的需求，需要执行一个命令或者脚本，但是需要几个小时甚至几天</span><span>。</span><span>这就要考虑一个问题，就是中途断网或出现其他意外情况，执行的任务中断了怎么办？你可以把命令或者脚本丢到后台运行，不过也不保险</span><span>。</span><span>笔者下面就介绍两种方法来避免这样的问题发生</span><span>。</span>

<span>**1\.** </span><span>**使用**</span><span>**nohup**</span>

<span>![15_242.png.jpg](images/15_242.png.jpg)</span>

<span>直接加一个</span><span>’&’</span><span>虽然丢到后台了，但是当退出该终端时很有可能这个脚本也会退出的，而在前面加上</span><span>’nohup’</span><span>就没有问题了</span><span>。nohup</span><span>的作用就是</span><span>不挂断地运行命令</span><span>。</span>

<span>**2\. screen**</span><span>**工具的使用**</span>

<span>简单来说，</span><span>screen</span><span>是一个可以在多个进程之间多路复用一个物理终端的窗口管理器</span><span>。screen</span><span>中有会话的概念，用户可以在一个</span><span>screen</span><span>会话中创建多个</span><span>screen</span><span>窗口，在每一个</span><span>screen</span><span>窗口中就像操作一个真实的</span><span>SSH</span><span>连接窗口那样</span><span>。</span><span>下面笔者介绍</span><span>screen</span><span>的一个简单应用</span><span>。</span>

<span>1</span><span>）</span><span>打开一个会话，直接输入</span><span>screen</span><span>命令然后回车，进入</span><span>screen</span><span>会话窗口</span><span>。</span><span>如果你没有</span><span>screen</span><span>命令，请用</span><span>’yum install -y screen’</span><span>安装</span><span>。</span>

<span>![15_243.png.jpg](images/15_243.png.jpg)</span>

<span>2</span><span>）</span><span>screen -ls</span> <span>查看已经打开的</span><span>screen</span><span>会话</span>

<span>![15_244.png.jpg](images/15_244.png.jpg)</span>

<span>3</span><span>）</span><span>Ctrl +a</span> <span>再按</span><span>d</span><span>退出该</span><span>screen</span><span>会话，只是退出，并没有结束</span><span>。</span><span>结束的话输入</span><span>Ctrl +d</span> <span>或者输入</span><span>exit</span>

<span>4</span><span>）退出后还想再次登录某个</span><span>screen</span><span>会话，使用</span><span>screen -r [screen</span> <span>编号</span><span>]</span><span>，这个编号就是上图中那个</span><span>2082\.</span> <span>当只有一个</span><span>screen</span><span>会话时，后面的编号是可以省略的</span><span>。</span>

<span>当你有某个需要长时间运行的命令或者脚本时就打开一个</span><span>screen</span><span>会话，然后运行该任务</span><span>。</span><span>按</span><span>ctrl +a</span> <span>再按</span><span>d</span><span>退出会话，不影响终端窗口上的任何操作</span><span>。</span>

<span> </span>

【**linux下同步时间服务器**】

<span>时间的准确性在服务器上非常重 要，所以要与标准时间保持同步，毕竟服务器的时钟并不一定精准，所以需要我们每隔一段时间去同步一下时间。笔者所管理的服务器每隔6小时就会同步一下时 间。如何同步呢？这就要用到ntpdate 这个指令。如果你的服务器上没有这个指令，请使用'yum install -y ntpdate'安装，或者下载源码包安装。

同步时间的命令为：'ntpdate  timeserver'  这里的timeserver为时间服务器的IP或者hostname，常用的timeserver有210.72.145.44, time.windows.com(windows的时间服务器)。如果你想每隔6小时同步一次那么请指定一个计划任务。

00 */6 * * *  /usr/sbin/ntpdate 210.72.145.44 >/dev/null

之所以在后面加一个重定向，是因为这个同步的过程是有内容输出的，因为我们的计划任务是在后台执行的，输出的内容会以邮件的形式发送给用户，所以为了避免邮件太多请输出到/dev/null （在linux下这个设备是虚拟的存在，你可以理解为空洞）</span>
