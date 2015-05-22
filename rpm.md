# 安装 RPM 包或者安装源码包 

<span>在</span><span>windows</span><span>下安装一个软件很轻松，只要双击</span><span>.exe</span><span>的文件，安装提示连续</span><span>“</span><span>下一步</span><span>”</span><span>即可，然而</span><span>linux</span><span>系统下安装一个软件似乎并不那么轻松了，因为我们不是在图形界面下</span><span>。</span><span>所以你要学会如何在</span><span>linux</span><span>下安装一个软件</span><span>。</span>

<span>在前面的内容中多次提到的</span><span>yum</span><span>，这个</span><span>yum</span><span>是</span><span>Redhat</span><span>所特有的安装</span><span>RPM</span><span>程序包的工具，使用起来相当方便</span><span>。</span><span>因为使用</span><span>RPM</span><span>安装某一个程序包有可能会因为该程序包依赖另一个程序包而无法安装</span><span>。</span><span>而使用</span><span>yum</span><span>工具就可以连同依赖的程序包一起安装</span><span>。</span><span>当然</span><span>CentOS</span><span>同样可以使用</span><span>yum</span><span>工具，而且在</span><span>CentOS</span><span>中你可以免费使用</span><span>yum</span><span>，但</span><span>Redhat</span><span>中只有当你付费后才能使用</span><span>yum</span><span>，默认是无法使用</span><span>yum</span><span>的</span><span>。</span><span>在介绍</span><span>yum</span><span>之前先说一说</span><span>RPM</span><span>相关的东西</span><span>。</span>

<span>【</span><span>**RPM**</span><span>**工具**</span><span>】</span>

<span>RPM</span><span>是</span><span>”Redhat Package Manager”</span><span>的缩写，根据名字也能猜到这是</span><span>Redhat</span><span>公司开发出来的</span><span>。RPM</span> <span>是以一种数据库记录的方式来将你所需要的套件安装到你的</span><span>Linux</span> <span>主机的一套管理程序</span><span>。</span><span>也就是说，你的</span><span>linux</span><span>系统中存在着一个关于</span><span>RPM</span><span>的数据库，它记录了安装的包以及包与包之间依赖相关性</span><span>。RPM</span><span>包是预先在</span><span>linux</span><span>机器上编译好并打包好的文件，安装起来非常快捷</span><span>。</span><span>但是也有一些缺点，比如安装的环境必须与编译时的环境一致或者相当；包与包之间存在着相互依赖的情况；卸载包时需要先把依赖的包卸载掉，如果依赖的包是系统所必须的，那就不能卸载这个包，否则会造成系统崩溃</span><span>。</span>

<span>如果你的光驱中还有系统安装盘的话，你可以通过</span><span>”mount /dev/cdrom /mnt”</span><span>命令把光驱挂载到</span><span>/mnt</span><span>目录下，那么你会在</span><span>/mnt/CentOS</span><span>目录下看到很多</span><span>.rpm</span><span>的文件，这就是</span><span>RPM</span><span>包了</span><span>。</span>

<span>![11_1.png.jpg](images/11_1.png.jpg)</span>

<span>每一个</span><span>rpm</span><span>包的名称都由</span><span>”-“</span><span>和</span><span>”.”</span><span>分成了若干部分</span><span>。</span><span>就拿</span> <span>a2ps-4.13b-57.2.el5.i386.rpm</span> <span>这个包来解释一下，</span><span>a2ps</span> <span>为包名；</span><span>4.13b</span><span>则为版本信息；</span><span>57.2.el5</span><span>为发布版本号；</span><span>i386</span><span>为运行平台</span><span>。</span><span>其中运行平台常见的有</span><span>i386, i586, i686, x86_64</span> <span>，需要你注意的是</span><span>cpu</span><span>目前是分</span><span>32</span><span>位和</span><span>64</span><span>位的，</span><span>i386,i586</span><span>和</span><span>i686</span><span>都为</span><span>32</span><span>位平台，</span><span>x86_64</span><span>则代表为</span><span>64</span><span>位的平台</span><span>。</span><span>另外有些</span><span>rpm</span><span>包并没有写具体的平台而是</span><span>noarch</span><span>，这代表这个</span><span>rpm</span><span>包没有硬件平台限制</span><span>。</span><span>例如</span> <span>alacarte-0.10.0-1.fc6.noarch.rpm 。</span><span>下面介绍一下</span><span>rpm</span><span>常用的命令</span><span>。</span>

<span>1</span><span>）安装一个</span><span>rpm</span><span>包</span>

<span>![11_7.png.jpg](images/11_7.png.jpg)</span>

<span>-i</span> <span>：安装的意思</span>

<span>-v</span> <span>：可视化</span>

<span>-h</span> <span>：显示安装进度</span>

<span>另外在安装一个</span><span>rpm</span><span>包时常用的附带参数有：</span>

<span>--force</span> <span>强制安装，即使覆盖属于其他包的文件也要安装</span>

<span>--nodeps</span> <span>当要安装的</span><span>rpm</span><span>包依赖其他包时，即使其他包没有安装，也要安装这个包</span>

<span>2</span><span>）升级一个</span><span>rpm</span><span>包</span>

<span>rpm -Uvh filename -U</span> <span>：即升级的意思</span>

<span>3</span><span>）卸载一个</span><span>rpm</span><span>包</span>

<span>rpm -e filename</span> <span>这里的</span><span>filename</span><span>是通过</span><span>rpm</span><span>的查询功能所查询到的，稍后会作介绍</span><span>。</span>

<span>![11_8.png.jpg](images/11_8.png.jpg)</span>

<span>卸载时后边跟的</span><span>filename</span><span>和安装时的是有区别的</span><span>。</span><span>上面命令提到的</span> <span>“|”</span><span>在</span><span>linux</span><span>系统中用的非常多也非常有用，它是一个管道符，用来把前面运行的结果传递给后面的命令</span><span>。</span><span>以后会做详细介绍，而后出现的</span><span>grep</span><span>命令则是用来过滤某个关键词的工具，在后续章节中会做详细介绍</span><span>。</span>

<span>4</span><span>）查询一个包是否安装</span>

<span>rpm -q rpm</span><span>包名（这里的包名，是不带有平台信息以及后缀名的）</span>

<span>![11_9.png.jpg](images/11_9.png.jpg)</span>

<span>如果加上了平台信息以及后缀名反而不能查出来</span><span>。</span><span>你还可以查询当前系统中所安装的所有</span><span>rpm</span><span>包</span><span>。</span>

<span>![11_10.png.jpg](images/11_10.png.jpg)</span>

<span>因为太多，所以笔者列出前十个</span><span>。</span>

<span>5</span><span>）得到一个</span><span>rpm</span><span>包的相关信息</span>

<span>rpm -qi</span> <span>包名</span><span>（同样不需要加平台信息与后缀名）</span>

<span>![11_11.png.jpg](images/11_11.png.jpg)</span>

<span>6</span><span>）列出一个</span><span>rpm</span><span>包安装的文件</span>

<span>rpm -ql</span> <span>包名</span>

<span>![11_21.png.jpg](images/11_21.png.jpg)</span>

<span>通过上面的命令可以看出</span><span>vim</span><span>是通过安装</span><span>vim-enhanced-7.0.109-6.el5</span><span>这个</span><span>rpm</span><span>包得来的</span><span>。</span><span>那么反过来如何通过一个文件去查找是由安装哪个</span><span>rpm</span><span>包得来的？</span>

<span>7</span><span>）列出某一个文件属于哪个</span><span>rpm</span><span>包</span>

<span>rpm -qf</span> <span>文件的绝对路径</span>

<span>![11_22.png.jpg](images/11_22.png.jpg)</span>

<span>前面讲过如何查找一个文件（可执行命令）的绝对路径</span>

<span>![11_23.png.jpg](images/11_23.png.jpg)</span>

<span>所以你也可以把这两条命令连起来写</span>

<span>![11_24.png.jpg](images/11_24.png.jpg)</span>

<span>看到了吗，</span><span>which vim</span> <span>这条命令是由两个反引号引起来的，这代表引用反引号里面的命令所产生的结果</span><span>。</span><span>关于</span><span>rpm</span><span>工具的使用还有很多内容，笔者就不一一列举了，只要你掌握上面这些内容，完全够你平时工作用的了</span><span>。</span>

<span>【</span><span>**yum**</span><span>**工具**</span><span>】</span>

<span>介绍完</span><span>rpm</span><span>工具后，还需要你掌握最常用的</span><span>yum</span><span>工具，这个工具比</span><span>rpm</span><span>工具好用多了，当然前提是你使用的</span><span>linux</span><span>系统是支持</span><span>yum</span><span>的</span><span>。yum</span><span>最大的优势在于可以联网去下载所需要的</span><span>rpm</span><span>包，然后自动安装，在这个工程中如果要安装的</span><span>rpm</span><span>包有依赖关系，</span><span>yum</span><span>会帮你解决掉这些依赖关系依次安装所有</span><span>rpm</span><span>包</span><span>。</span><span>下面笔者介绍常用的</span><span>yum</span> <span>命令</span><span>。</span>

<span>1</span><span>）</span><span>列出所有可用的</span><span>rpm</span><span>包</span> <span>“yum list “</span>

<span>![11_25.png.jpg](images/11_25.png.jpg)</span>

<span>限于篇幅，笔者只列举出来前</span><span>7</span><span>个包信息</span><span>。</span><span>从上例中可以看到有</span><span>”mirrors.163.com”</span><span>信息出现，这是在告诉用户，它是从</span><span>mirrors.163.com</span><span>这里下载到的</span><span>rpm</span><span>包资源</span><span>。</span><span>如果你使用的是</span><span>CentOS</span><span>则你可以从</span><span>/etc/yum.repos.d/CentOS-Base.repo</span><span>这个文件下看到相关的配置信息</span><span>。</span><span>从上面的例子中你还可以看到最左侧是</span><span>rpm</span><span>包名字，中间是版本信息，最右侧是安装信息，如果安装了就显示</span><span>installed</span><span>，未安装则显示</span><span>base</span><span>或者</span><span>extras</span><span>，如果是该</span><span>rpm</span><span>包已安装但需要升级则显示</span><span>updates。</span>

<span>2</span><span>）搜索一个</span><span>rpm</span><span>包</span> <span>“yum search [</span><span>相关关键词</span><span>]”</span>

<span>![11_26.png.jpg](images/11_26.png.jpg)</span>

<span>除了这样搜索外，笔者常用的是利用</span><span>grep</span><span>来过滤</span>

<span>![11_27.png.jpg](images/11_27.png.jpg)</span>

<span>相信你也会喜欢用后者吧，这样看起来简明的多</span><span>。</span>

<span>3</span><span>）安装一个</span><span>rpm</span><span>包</span> <span>“yum install [-y] [rpm</span><span>包名</span><span>]”</span>

<span>如果不加</span><span>-y</span><span>选项，则会以与用户交互的方式安装，首先是列出需要安装的</span><span>rpm</span><span>包信息，然后会问用户是否需要安装，输入</span><span>y</span><span>则安装，输入</span><span>n</span><span>则不安装</span><span>。</span><span>而笔者嫌这样太麻烦，所以直接加上</span><span>-y</span><span>选项，这样就省略掉了问用户是否安装的那一步</span><span>。![11_28.png.jpg](images/11_28.png.jpg)</span>

<span>4</span><span>）卸载一个</span><span>rpm</span><span>包</span> <span>“yum remove [-y] [rpm</span><span>包名</span><span>]”</span>

<span>![11_29.png.jpg](images/11_29.png.jpg)</span>

<span>卸载和安装一样，你也可以直接加上</span><span>-y</span><span>选项来省略掉和用户交互的步骤</span><span>。</span><span>在这里笔者要提醒你一下，卸载某个</span><span>rpm</span><span>包一定要看清楚了，不要连其他重要的</span><span>rpm</span><span>包一起卸载了，以免影响正常的业务</span><span>。</span>

<span>4</span><span>）升级一个</span><span>rpm</span><span>包</span> <span>“yum update [-y] [rpm</span><span>包</span><span>]”</span>

<span>![11_44.png.jpg](images/11_44.png.jpg)</span>

<span>以上介绍了如何使用</span><span>yum</span><span>搜索</span><span>、</span><span>安装</span><span>、</span><span>卸载以及升级一个</span><span>rpm</span><span>包，如果你掌握了这些那么你就已经可以解决日常工作中遇到的与</span><span>rpm</span><span>包相关问题了</span><span>。</span><span>当然</span><span>yum</span><span>工具还有好多其他好用的命令，笔者不在列举出来，如果你感兴趣就去</span><span>man</span><span>一下吧</span><span>。</span><span>除此之外，笔者还会教你一些关于</span><span>yum</span><span>的小应用</span><span>。</span>

<span>**1** </span><span>**使用本地的光盘来制作一个**</span><span>**yum**</span><span>**源**</span>

<span>有时候你的</span><span>linux</span><span>系统不能联网，当然就不能很便捷的使用联网的</span><span>yum</span><span>源了，这时候就需要你自己会利用</span><span>linux</span><span>系统光盘制作一个</span><span>yum</span><span>源</span><span>。</span><span>具体步骤如下：</span>

<span>a.</span><span>挂载光盘</span>

<span>[root@fortest Server]# mount -t iso9660 -o loop /dev/cdrom /mnt</span>

<span>b.</span><span>删除</span><span>/etc/yum.repos.d</span><span>目录所有的</span><span>repo</span><span>文件</span>

<span>[root@fortest Server]# rm -rf /etc/yum.repos.d/*</span>

<span>c.</span><span>创建新文件</span><span>dvd.repo</span>

<span>[root@fortest Server]# vim /etc/yum.repos.d/dvd.repo</span>

<span>加入以下内容：</span>

<span>[dvd]</span>

<span>name=install dvd</span>

<span>baseurl=file:///mnt</span>

<span>enabled=1</span>

<span>gpgcheck=0</span>

<span>d.</span><span>刷新</span><span>repos,</span><span>生成缓存</span>

<span>[root@fortest Server]#yum makecache</span>

<span>然后就可以使用</span><span>yum</span><span>命令安装你所需要的软件包了</span>

<span>**2** </span><span>**利用**</span><span>**yum**</span><span>**工具下载一个**</span><span>**rpm**</span><span>**包**</span>

<span>有时，我们需要下载一个</span><span>rpm</span><span>包，只是下载下来，拷贝给其他机器使用，前面也介绍过</span><span>yum</span><span>安装</span><span>rpm</span><span>包的时候，首先得下载这个</span><span>rpm</span><span>包然后再去安装，所以使用</span><span>yum</span><span>完全可以做到只下载而不安装</span><span>。</span>

<span>a.</span> <span>首选要安装</span> <span>yum-downloadonly</span>

<span># yum install -y yum-downloadonly.noarch</span>

<span>b.</span> <span>下载一个</span><span>rpm</span><span>包而不安装</span>

<span># yum install test.rpm -y --downloadonly //</span><span>这样虽然下载了，但是并没有保存到我们想要的目录下，那么如何指定目录呢？</span>

<span>c.</span> <span>下载到指定目录</span>

<span># yum install test.rpm -y --downloadonly --downloaddir=/usr/local/src</span>

<span>![11_45.png.jpg](images/11_45.png.jpg)</span>

<span>【</span><span>**安装源码包**</span><span>】</span>

<span>其实，在</span><span>linux</span><span>下面安装一个源码包是最常用的，笔者在日常的管理工作中，大部分软件都是通过源码安装的</span><span>。</span><span>安装一个源码包，是需要我们自己把源代码编译成二进制的可执行文件</span><span>。</span><span>如果你读得懂这些源代码，那么你就可以去修改这些源代码自定义功能，然后再去编译成你想要的</span><span>。</span><span>使用源码包的好处除了可以自定义修改源代码外还可以定制相关的功能，因为源码包在编译的时候是可以附加额外的选项的</span><span>。</span>

<span>源码包的编译用到了</span><span>linux</span><span>系统里的编译器，常见的源码包一般都是用</span><span>C</span><span>语言开发的，这也是因为</span><span>C</span><span>语言为</span><span>linux</span><span>上最标准的程序语言</span><span>。Linux</span><span>上的</span><span>C</span><span>语言编译器叫做</span><span>gcc</span><span>，利用它就可以把</span><span>C</span><span>语言变成可执行的二进制文件</span><span>。</span><span>所以如果你的机器上没有安装</span><span>gcc</span><span>就没有办法去编译源码</span><span>。</span><span>你可以使用</span> <span>yum install -y gcc</span> <span>来完成安装</span><span>。</span>

<span>安装一个源码包，通常需要三个步骤：</span>

<span>1\. ./config</span> <span>在这一步可以定制功能，加上相应的选项即可，具有有什么选项可以通过</span><span>”./config --help ”</span><span>命令来查看</span><span>。</span><span>在这一步会自动检测你的</span><span>linux</span><span>系统与相关的套件是否有编译该源码包时需要的库，因为一旦缺少某个库就不能完成编译</span><span>。</span><span>只有检测通过后才会生成一个</span><span>Makefile</span><span>文件</span><span>。</span>

<span>2\. make</span> <span>使用这个命令会根据</span><span>Makefile</span><span>文件中预设的参数进行编译，这一步其实就是</span><span>gcc</span><span>在工作了</span><span>。</span>

<span>3\. make install</span> <span>安装步骤，生成相关的软件存放目录和配置文件的过程</span><span>。</span>

<span>上面介绍的</span><span>3</span><span>步并不是所有的源码包软件都一样的，笔者以前也曾经遇到过，安装步骤并不是这样，也就是说源码包的安装并非具有一定的标准安装步骤</span><span>。</span><span>这就需要你拿到源码包解压后，然后进入到目录找相关的帮助文档，通常会以</span><span>INSTALL</span><span>或者</span><span>README</span><span>为文件名</span><span>。</span><span>所以，你一定要去看一下</span><span>。</span><span>下面笔者会编译安装一个源码包来帮你更深刻的去理解如何安装源码包</span><span>。</span>

<span>1\.</span> <span>下载一个源码包</span>

<span>![11_46.png.jpg](images/11_46.png.jpg)</span>

<span>这里要提一下，建议以后你把所有下载的源码包放到</span><span>/usr/local/src/</span><span>目录下，这个并不是必须的，只是一个约定</span><span>。</span><span>方便你和你的同事将来更好的去运维这台服务器</span><span>。wget</span><span>即为下载的命令，后边跟源码包的下载地址</span><span>。</span><span>该地址为笔者从网上找的一个</span><span>apache</span><span>的下载地址</span><span>。</span>

<span>2\.</span> <span>解压源码包</span>

<span>![11_47.png.jpg](images/11_47.png.jpg)</span>

<span>一般的源码包都是一个压缩包，如何解压一个</span><span>.tar.gz</span><span>的包上一章讲过的</span><span>。</span>

<span>3\.</span> <span>配置相关的选项，并生成</span><span>Makefile</span>

<span>![11_48.png.jpg](images/11_48.png.jpg)</span>

<span>使用</span><span>./config --help</span> <span>可以查看可用的选项</span><span>。</span><span>一般常用的有</span><span>”--prefix=PREFIX “</span> <span>这个选项的意思是定义软件包安装到哪里</span><span>。</span><span>到这里，笔者再提一个小小的约定，通常源码包都是安装在</span><span>/usr/local/</span><span>目录下的</span><span>。</span><span>比如，我们把</span><span>apache</span><span>安装在</span><span>/usr/local/apache2</span><span>下，那么这里就应该这样写</span><span>” --prefix=/usr/local/apache2”。</span><span>其他还有好多选项，如果你有耐心你可以挨个去看一看都有什么作用</span><span>。</span>

<span>![11_49.png.jpg](images/11_49.png.jpg)</span>

<span>笔者在这里只定义了</span><span>apache</span><span>的安装目录，其他都是默认</span><span>。</span><span>回车后，开始执行</span><span>check</span><span>操作</span><span>。</span>

<span>![11_50.png.jpg](images/11_50.png.jpg)</span>

<span>等</span><span>check</span><span>结束后生成了</span><span>Makefile</span><span>文件</span>

<span>![11_51.png.jpg](images/11_51.png.jpg)</span>

<span>除了查看有没有生成</span><span>Makefile</span><span>文件来判定有没有完成</span><span>./config</span> <span>的操作外，还可以通过这个命令</span><span>”echo $?”</span><span>来判定，如果是</span><span>0</span><span>，则表示上一步操作成功完成，否则就是没有成功</span><span>。</span>

<span>![11_52.png.jpg](images/11_52.png.jpg)</span>

<span>4\.</span> <span>进行编译</span>

<span>![11_53.png.jpg](images/11_53.png.jpg)</span>

<span>这一步操作，就是把源代码编译成二进制的可执行文件，这一步也是最漫长的一步，编译时间的长短取决于源代码的多少和机器配置</span><span>。</span>

<span>5\.</span> <span>安装</span>

<span>![11_54.png.jpg](images/11_54.png.jpg)</span>

<span>在安装前，先确认上一步操作是否成功完成</span><span>。</span>

<span>![11_55.png.jpg](images/11_55.png.jpg)</span>

<span>make install</span> <span>会创建相应的目录以及文件</span><span>。</span><span>当完成安装后，会在</span><span>/usr/local</span><span>目录下多了一个</span><span>apache2</span><span>目录，这就是</span><span>apache</span><span>所安装的目录了</span><span>。</span>

<span>![11_56.png.jpg](images/11_56.png.jpg)</span>

<span>其实在日常的源码安装工作中，并不是每个都像笔者这样顺利完成安装的，遇到错误不能完成安装的情况是很多的</span><span>。</span><span>通常都是因为缺少某一个库文件导致的</span><span>。</span><span>这就需要你仔细琢磨报错信息或者查看当前目录下的</span><span>config.log</span><span>去得到相关的信息</span><span>。</span><span>另外，如果自己不能解决那就去网上</span><span>google</span><span>一下吧，通常你会得到你想要的答案</span><span>。</span>

