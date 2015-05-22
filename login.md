# Linux 系统的远程登录

<span>首先要说一下，该部分内容对于</span><span>linux</span><span>初学者来讲并不是特别重要的，可以先跳过该章节，先学下一章，等学完后再回来看这一章</span><span>。</span>

<span> Linux </span><span>大多应用于服务器，而服务器不可能像</span><span> PC </span><span>一样放在办公室，它们是放在</span><span> IDC </span><span>机房的，所以我平时登录</span><span> linux </span><span>系统都是通过远程登录的</span><span>。Linux </span><span>系统中是通过</span><span> ssh </span><span>服务实现的远程登录功能</span><span>。</span><span>默认</span><span> ssh </span><span>服务开启了</span><span> 22 </span><span>端口，而且当我们安装完系统时，这个服务已经安装，并且是开机启动的</span><span>。</span><span>所以不需要我们额外配置什么就能直接远程登录</span><span>linux</span><span>系统</span><span>。ssh</span><span>服务的配置文件为</span> <span> /etc/ssh/sshd_config </span><span>，你可以修改这个配置文件来实现你想要的</span><span> ssh </span><span>服务</span><span>。</span><span>比如你可以更改启动端口为</span><span> 36000. </span>

<span>如果你是</span><span> Windows </span><span>的操作系统，则</span><span>Linux</span><span>远程登录需要在我们的机器上额外安装一个终端软件</span><span>。</span><span>目前比较常见的终端登录软件有</span><span>SecureCRT, Putty, SSH Secure Shell</span><span>等，很多朋友喜欢用</span><span>SecureCRT</span><span>因为它的功能是很强大的，而笔者喜欢用</span><span> Putty </span><span>，只是因为它的小巧以及非常漂亮的颜色显示</span><span>。</span><span>不管你使用哪一个客户端软件，最终的目的只有一个，就是远程登录到</span><span> linux </span><span>服务器上</span><span>。</span><span>这些软件网上有很多免费版的，你可以下载一个试着玩玩</span><span>。</span><span>下面笔者介绍如何使用</span><span>Putty</span><span>登录远程</span><span>linux</span><span>服务器</span><span>。</span>

<span>如果你下载了</span><span>putty</span><span>，请双击</span><span>putty.exe</span> <span>然后弹出如下的窗口</span><span>。</span><span>笔者所用</span><span>putty</span><span>为英文版的，如果你觉得英文的用着别扭，可以下载一个中文版的</span><span>。</span>

<span>![5_1.png.jpg](images/5_1.png.jpg)</span>

<span>因为是远程登录，所以你要登录的服务器一定会有一个</span><span>IP</span><span>或者主机名</span><span>。</span><span>请在</span><span>Host Name( or IP address)</span> <span>下面的框中输入你要登录的远程服务器</span><span>IP(</span><span>如果你的</span><span>linux</span><span>还没有</span><span>IP</span><span>，那么请自行设置一个</span><span>IP</span><span>，如何设置请到后续章节查找</span><span>)</span><span>，然后回车</span><span>。</span>

<span>![5_12.png.jpg](images/5_12.png.jpg)</span>

<span>此时，提示我们输入要登录的用户名</span><span>。</span>

<span>![5_13.png.jpg](images/5_13.png.jpg)</span>

<span>输入</span><span>root</span> <span>然后回车，再输入密码，就能登录到远程的</span><span>linux</span><span>系统了</span><span>。</span>

<span>![5_14.png.jpg](images/5_14.png.jpg)</span>

## 使用密钥认证机制远程登录 linux

<span>SSH</span><span>服务支持一种安全认证机制，即密钥认证</span><span>。</span><span>所谓的密钥认证，实际上是使用一对加密字符串，一个称为公钥</span><span>(public key)</span><span>，</span><span>任何人都可以看到其内容，用于加密；另一个称为密钥</span><span>(private key)</span><span>，只有拥有者才能看到，用于解密</span><span>。</span> <span>通过公钥加密过的密文使用密钥可以轻松解密，但根据公钥来猜测密钥却十分困难</span><span>。 ssh</span> <span>的密钥认证就是使用了这一特性</span><span>。</span><span>服务器和客户端都各自拥有自己的公钥和密钥</span><span>。</span> <span>如何使用密钥认证登录</span><span>linux</span><span>服务器呢？</span>

<span>首先使用工具</span> <span>PUTTYGEN.EXE</span> <span>生成密钥对</span><span>。</span><span>打开工具</span><span>PUTTYGEN.EXE</span><span>后如下图所示：</span>

<span>![5_15.png.jpg](images/5_15.png.jpg)</span>

<span>该工具可以生成三种格式的</span><span>key</span> <span>：</span><span>SSH-1(RSA) SSH-2(RSA) SSH-2(DSA)</span> <span>，我们采用默认的格式即</span><span>SSH-2(RSA)。Number of bits in a generated key</span> <span>这个是指生成的</span><span>key</span><span>的大小，这个数值越大，生成的</span><span>key</span><span>就越复杂，安全性就越高</span><span>。</span><span>这里我们写</span><span>2048.</span>

<span>![5_16.png.jpg](images/5_16.png.jpg)</span>

<span>然后单击</span><span>Generate</span> <span>开始生成密钥对：</span>

<span>![5_17.png.jpg](images/5_17.png.jpg)</span>

<span>注意的是，在这个过程中鼠标要来回的动，否则这个进度条是不会动的</span><span>。</span>

<span>![5_18.png.jpg](images/5_18.png.jpg)</span>

<span>到这里，密钥对已经生成了</span><span>。</span><span>你可以给你的密钥输入一个密码，（在</span><span>Key Passphrase</span><span>那里）也可以留空</span><span>。</span><span>然后点</span> <span>Save public key</span> <span>保存公钥，点</span> <span>Save private Key</span> <span>保存私钥</span><span>。</span><span>笔者建议你放到一个比较安全的地方，一来防止别人偷窥，二来防止误删除</span><span>。</span><span>接下来就该到远程</span><span>linux</span><span>主机上设置了</span><span>。</span>

<span>1</span><span>）创建目录</span> <span>/root/.ssh</span> <span>并设置权限</span>

<span>[root@localhost ~]# mkdir /root/.ssh mkdir</span> <span>命令用来创建目录，以后会详细介绍，暂时只了解即可</span><span>。</span>

<span>[root@localhost ~]# chmod 700 /root/.ssh chmod</span> <span>命令是用来修改文件属性权限的，以后会详细介绍</span><span>。</span>

<span>2</span><span>）创建文件</span> <span>/ root/.ssh/authorized_keys</span>

<span>[root@localhost ~]# vim /root/.ssh/authorized_keys vim</span> <span>命令是编辑一个文本文件的命令，同样在后续章节详细介绍</span><span>。</span>

<span>3</span><span>）打开刚才生成的</span><span>public key</span> <span>文件，建议使用写字板打开，这样看着舒服一些，复制从</span><span>AAAA</span><span>开头至</span> <span>“</span><span>---- END SSH2 PUBLIC KEY ----</span><span>“</span> <span>该行上的所有内容，粘贴到</span><span>/root/.ssh/authorized_keys</span> <span>文件中，要保证所有字符在一行</span><span>。</span><span>（可以先把复制的内容拷贝至记事本，然后编辑成一行载粘贴到该文件中）</span><span>。</span><span>在这里要简单介绍一下，如何粘贴，用</span><span>vim</span><span>打开那个文件后，该文件不存在，所以</span><span>vim</span><span>会自动创建</span><span>。</span><span>按一下字母</span><span>”i”</span><span>然后同时按</span><span>shift + Insert</span> <span>进行粘贴（或者单击鼠标邮件即可），前提是已经复制到剪切板中了</span><span>。</span><span>粘贴好后，然后把光标移动到该行最前面输入</span><span>ssh-ras</span> <span>，然后按空格</span><span>。</span><span>再按</span><span>ESC</span><span>，然后输入冒号</span><span>wq</span> <span>即</span> <span>:wq</span> <span>就保存了</span><span>。</span><span>格式如下图：</span>

<span>![5_19.png.jpg](images/5_19.png.jpg)</span>

<span>4</span><span>）再设置</span><span>putty</span><span>选项，点窗口左侧的</span><span>SSh –> Auth</span> <span>，单击窗口右侧的</span><span>Browse…</span> <span>选择刚刚生成的私钥，</span><span>再点</span><span>Open</span> <span>，此时输入</span><span>root</span><span>，就不用输入密码就能登录了</span><span>。</span>

<span>![5_20.png.jpg](images/5_20.png.jpg)</span>

<span>如果在前面你设置了</span><span>Key Passphrase</span> <span>，那么此时就会提示你输入密码的</span><span>。</span><span>为了更加安全建议大家要设置一个</span><span>Key Passphrase。</span>

