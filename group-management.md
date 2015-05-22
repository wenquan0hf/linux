# linux 系统用户以及用户组管理 

<span>关于这部分内容，笔者在日常的</span><span>linux</span><span>系统管理工作中用到的并不多，但这并不代表该内容不重要</span><span>。</span><span>毕竟</span><span>linux</span><span>系统是一个多用户的系统，每个账号都干什么用，你必须了如指掌</span><span>。</span><span>因为这涉及到一个安全的问题</span><span>。</span>

<span>**【**</span><span>**认识**</span><span>**/etc/passwd**</span><span>**和**</span><span>**/etc/shadow】**</span>

<span>这两个文件可以说是</span><span>linux</span><span>系统中最重要的文件之一</span><span>。</span><span>如果没有这两个文件或者这两个文件出问题，则你是无法正常登录</span><span>linux</span><span>系统的</span><span>。</span>

<span>![7_1.png.jpg](images/7_1.png.jpg)</span>

<span>/etc/passwd</span><span>由</span><span>’:’</span><span>分割成</span><span>7</span><span>个字段，每个字段的具体含义是：</span>

<span>1</span><span>）用户名（如第一行中的</span><span>root</span><span>就是用户名），代表用户账号的字符串</span><span>。</span><span>用户名字符可以是大小写字母</span><span>、</span><span>数字</span><span>、</span><span>减号（不能出现在首位）</span><span>、</span><span>点以及下划线，其他字符不合法</span><span>。</span><span>虽然用户名中可以出现点，但不建议使用，尤其是首位为点时，另外减号也不建议使用，因为容易造成混淆</span><span>。</span>

<span>2</span><span>）存放的就是该账号的口令，为什么是</span><span>’x’</span><span>呢？早期的</span><span>unix</span><span>系统口令确实是存放在这里，但基于安全因素，后来就将其存放到</span><span>/etc/shadow</span><span>中了，在这里只用一个</span><span>’x’</span><span>代替</span><span>。</span>

<span>3</span><span>）这个数字代表用户标识号，也叫做</span><span>uid。</span><span>系统识别用户身份就是通过这个数字来的，</span><span>0</span><span>就是</span><span>root</span><span>，也就是说你可以修改</span><span>test</span><span>用户的</span><span>uid</span><span>为</span><span>0</span><span>，那么系统会认为</span><span>root</span><span>和</span><span>test</span><span>为同一个账户</span><span>。</span><span>通常</span><span>uid</span><span>的取值范围是</span><span>0~65535</span><span>，</span><span>0</span><span>是超级用户（</span><span>root</span><span>）的标识号，</span><span>1~499</span><span>由系统保留，作为管理账号，普通用户的标识号从</span><span>500</span><span>开始，如果我们自定义建立一个普通用户，你会看到该账户的标识号是大于或等于</span><span>500</span><span>的</span><span>。</span>

<span>4</span><span>）表示组标识号，也叫做</span><span>gid。</span><span>这个字段对应着</span><span>/etc/group</span> <span>中的一条记录，其实</span><span>/etc/group</span><span>和</span><span>/etc/passwd</span><span>基本上类似</span><span>。</span>

<span>5</span><span>）注释说明，该字段没有实际意义，通常记录该用户的一些属性，例如姓名</span><span>、</span><span>电话</span><span>、</span><span>地址等等</span><span>。</span><span>不过，当你使用</span><span>finger</span><span>的功能时就会显示这些信息的（稍后做介绍）</span><span>。</span>

<span>6</span><span>）用户的家目录，当用户登录时就处在这个目录下</span><span>。root</span><span>的家目录是</span><span>/root</span><span>，普通用户的家目录则为</span><span>/home/username</span><span>，这个字段是可以自定义的，比如你建立一个普通用户</span><span>test1</span><span>，要想让</span><span>test1</span><span>的家目录在</span><span>/data</span><span>目录下，只要修改</span><span>/etc/passwd</span><span>文件中</span><span>test1</span><span>那行中的该字段为</span><span>/data</span><span>即可</span><span>。</span>

<span>7</span><span>）</span><span>shell</span><span>，用户登录后要启动一个进程，用来将用户下达的指令传给内核，这就是</span><span>shell。Linux</span><span>的</span><span>shell</span><span>有很多种</span><span>sh, csh, ksh, tcsh, bash</span><span>等，而</span><span>Redhat/CentOS</span><span>的</span><span>shell</span><span>就是</span><span>bash。</span><span>查看</span><span>/etc/passwd</span><span>文件，该字段中除了</span><span>/bin/bash</span><span>外还有</span><span>/sbin/nologin</span><span>比较多，它表示不允许该账号登录</span><span>。</span><span>如果你想建立一个账号不让他登录，那么就可以把该字段改成</span><span>/sbin/nologin</span><span>，默认是</span><span>/bin/bash。</span>

<span>![7_12.png.jpg](images/7_12.png.jpg)</span>

<span>再来看看</span><span>/etc/shadow</span><span>这个文件，和</span><span>/etc/passwd</span><span>类似，用</span><span>”:”</span><span>分割成</span><span>9</span><span>个字段</span><span>。</span>

<span>1</span><span>）用户名，跟</span><span>/etc/passwd</span><span>对应</span><span>。</span>

<span>2</span><span>）用户密码，这个才是该账号的真正的密码，不过这个密码已经加密过了，但是有些黑客还是能够解密的</span><span>。</span><span>所以为了安全，该文件属性设置为</span><span>600</span><span>，只允许</span><span>root</span><span>读写</span><span>。</span>

<span>3</span><span>）上次更改密码的日期，这个数字是这样计算得来的，距离</span><span>1970</span><span>年</span><span>1</span><span>月</span><span>1</span><span>日到上次更改密码的日期，例如上次更改密码的日期为</span><span>2012</span><span>年</span><span>1</span><span>月</span><span>1</span><span>日，则这个值就是</span><span>365*</span><span>（</span><span>2012-1970</span><span>）</span><span>+1=15331。</span>

<span>4</span><span>）要过多少天才可以更改密码，默认是</span><span>0</span><span>，即不限制</span><span>。</span>

<span>5</span><span>）密码多少天后到期</span><span>。</span><span>即在多少天内必须更改密码，例如这里设置成</span><span>30</span><span>，则</span><span>30</span><span>天内必须更改一次密码，否则将不能登录系统，默认是</span><span>99999</span><span>，可以理解为永远不需要改</span><span>。</span>

<span>6</span><span>）密码到期前的警告期限，若这个值设置成</span><span>7</span><span>，则表示当</span><span>7</span><span>天后密码过期时，系统就发出警告告诉用户，提醒用户他的密码将在</span><span>7</span><span>天后到期</span><span>。</span>

<span>7</span><span>）账号失效期限</span><span>。</span><span>你可以这样理解，如果设置这个值为</span><span>3</span><span>，则表示：密码已经到期，然而用户并没有在到期前修改密码，那么再过</span><span>3</span><span>天，则这个账号就失效了，即锁定了</span><span>。</span>

<span>8</span><span>）账号的生命周期，跟第三段一样，是按距离</span><span>1970</span><span>年</span><span>1</span><span>月</span><span>1</span><span>日多少天算的</span><span>。</span><span>它表示的含义是，账号在这个日期前可以使用，到期后账号作废</span><span>。</span>

<span>9</span><span>）作为保留用的，没有什么意义</span><span>。</span>

<span>**【**</span><span>**新增**</span><span>**/**</span><span>**删除用户和用户组**</span><span>**】**</span>

<span>a.</span> <span>新增一个组</span> <span>groupadd [-g GID] groupname</span>

<span>![7_13.png.jpg](images/7_13.png.jpg)</span>

<span>不加</span><span>-g</span> <span>则按照系统默认的</span><span>gid</span><span>创建组，跟用户一样，</span><span>gid</span><span>也是从</span><span>500</span><span>开始的</span>

<span>![7_14.png.jpg](images/7_14.png.jpg)</span>

<span>-g</span><span>选项可以自定义</span><span>gid</span>

<span>b.</span> <span>删除组</span> <span>gropudel groupname</span>

<span>![7_15.png.jpg](images/7_15.png.jpg)</span>

<span>没有特殊选项</span><span>。</span>

<span>c.</span> <span>增加用户</span> <span>useradd [-u UID] [-g GID] [-d HOME] [-M] [-s]</span>

<span>-u</span> <span>自定义</span><span>UID</span>

<span>-g</span> <span>使其属于已经存在的某个</span><span>GID</span>

<span>-d</span> <span>自定义用户的家目录</span>

<span>-M</span> <span>不建立家目录</span>

<span>-s</span> <span>自定义</span><span>shell</span>

<span>![7_16.png.jpg](images/7_16.png.jpg)</span>

<span>你会发现，创建</span><span>test11</span><span>时，加上了</span><span>-M</span><span>选项后，在</span><span>/etc/passwd</span><span>文件中</span><span>test11</span><span>那行的第六字段依然有</span><span>/home/test11</span><span>，可是</span><span>ls</span><span>查看该目录时，会提示该目录不存在</span><span>。</span>

<span>![7_17.png.jpg](images/7_17.png.jpg)</span>

<span>-M</span><span>选项的作用就是不创建用户的家目录</span><span>。</span>

<span>-d.</span> <span>删除用户</span> <span>userdel [-r] username</span>

<span>![7_18.png.jpg](images/7_18.png.jpg)</span>

<span>-r</span> <span>选项的作用是删除用户时，连同用户的家目录一起删除</span><span>。</span>

<span>**【chfn** </span><span>**更改用户的**</span><span>**finger** </span><span>**（不常用）**</span><span>**】**</span>

<span>前面内容中提到了</span><span>findger</span><span>，即在</span><span>/etc/passwd</span><span>文件中的第</span><span>5</span><span>个字段中所显示的信息，那么如何去设定这个信息呢？</span>

<span>![7_19.png.jpg](images/7_19.png.jpg)</span>

<span>就是</span><span>chfn</span><span>这个命令了</span><span>。</span><span>修改完后，就会在</span><span>/etc/passwd</span><span>文件中的</span><span>test</span><span>的那一行第五个字段中看到相关信息了，默认是空的</span><span>。</span>

<span>**【**</span><span>**创建**</span><span>**/**</span><span>**修改一个用户的密码**</span><span> **“passwd [username]”】**</span>

<span>等创建完账户后，默认是没有设置密码的，虽然没有密码，但该账户同样登录不了系统</span><span>。</span><span>只有设置好密码后方可登录系统</span><span>。</span>

<span>为用户创建密码时，为了安全起见，请尽量设置复杂一些</span><span>。</span><span>你可以按照这样的规则来设置密码：</span><span>a.</span> <span>长度大于</span><span>10</span><span>个字符；</span><span>b.</span> <span>密码中包含大小写字母数字以及特殊字符（</span><span>*&</span><span>等）；</span><span>c.</span> <span>不规则性（不要出现</span><span>root, happy, love, linux, 123456, 111111</span><span>等等单词或者数字）；</span><span>d.</span> <span>不要带有自己名字</span><span>、</span><span>公司名字</span><span>、</span><span>自己电话</span><span>、</span><span>自己生日等</span><span>。</span>

<span>![7_20.png.jpg](images/7_20.png.jpg)</span>

<span>passwd</span> <span>后面不跟用户名则是更改当前用户的密码，当前用户为</span><span>root</span><span>，所以此时修改的是</span><span>root</span><span>的密码，后面跟</span><span>test</span><span>则修改的是</span><span>test</span><span>的密码</span><span>。</span>

<span>**【**</span><span>**用户身份切换**</span><span>**】**</span>

<span>Linux</span><span>系统中，有时候普通用户有些事情是不能做的，除非是</span><span>root</span><span>用户才能做到</span><span>。</span><span>这时就需要临时切换到</span><span>root</span><span>身份来做事了</span><span>。</span>

<span>![7_21.png.jpg](images/7_21.png.jpg)</span>

<span>用</span><span>test</span><span>账号登录</span><span>linux</span><span>系统，然后使用</span><span>su -</span> <span>就可以切换成</span><span>root</span><span>身份，前提是知道</span><span>root</span><span>的密码</span><span>。</span>

<span>![7_29.png.jpg](images/7_29.png.jpg)</span>

<span>你可以使用</span><span>echo $LOGNAME</span><span>来查看当前登录的用户名</span>

<span>![7_30.png.jpg](images/7_30.png.jpg)</span>

<span>su</span> <span>的语法为：</span> <span>su [-] username</span>

<span>后面可以跟</span><span>”-”</span><span>也可以不跟，普通用户</span><span>su</span><span>不加</span><span>username</span><span>时就是切换到</span><span>root</span><span>用户，当然</span><span>root</span><span>用户同样可以</span><span>su</span><span>到普通用户</span><span>。</span>

<span>![7_31.png.jpg](images/7_31.png.jpg)</span>

<span>加</span><span>”-“</span><span>后会连同用户的环境变量一起切换过来</span><span>。su test</span> <span>后虽然切换到了</span><span>test</span><span>用户，但是当前目录还是切换前的</span><span>/root</span><span>目录，然后当用</span><span>su - test</span><span>时切换用户后则到了</span><span>test</span><span>的家目录</span><span>/home/test。</span><span>当用</span><span>root</span><span>切换普通用户时，是不需要输入密码的</span><span>。</span><span>这也体现了</span><span>root</span><span>用户至高无上的权利</span><span>。</span>

<span>用</span><span>su</span><span>是可以切换用户身份，如果每个普通用户都能切换到</span><span>root</span><span>身份，如果某个用户不小心泄漏了</span><span>root</span><span>的密码，那岂不是系统非常的不安全？没有错，为了改进这个问题，产生了</span><span>sudo</span><span>这个命令</span><span>。</span><span>使用</span><span>sudo</span><span>执行一个</span><span>root</span><span>才能执行的命令是可以办到的，但是需要输入密码，这个密码并不是</span><span>root</span><span>的密码而是用户自己的密码</span><span>。</span><span>默认只有</span><span>root</span><span>用户能使用</span><span>sudo</span><span>命令，普通用户想要使用</span><span>sudo</span><span>，是需要</span><span>root</span><span>预先设定的，即，使用</span><span>visudo</span><span>命令去编辑相关的配置文件</span><span>/etc/sudoers。</span><span>如果没有</span><span>visudo</span><span>这个命令，请使用</span><span>” yum install -y sudo”</span><span>安装</span><span>。</span>

<span>![7_32.png.jpg](images/7_32.png.jpg)</span>

<span>默认</span><span>root</span><span>能够</span><span>sudo</span><span>是因为这个文件中有一行</span><span>” root ALL=(ALL) ALL”</span> <span>在该行下面加入</span><span>” test ALL=(ALL) ALL”</span><span>就可以让</span><span>test</span><span>用户拥有了</span><span>sudo</span><span>的权利</span><span>。</span><span>如果每增加一用户就设置一行，这样太麻烦了</span><span>。</span><span>所以你可以这样设置</span><span>。</span>

<span>![7_33.png.jpg](images/7_33.png.jpg)</span>

<span>把这一行前面的</span><span>”#”</span><span>去掉，让这一行生效</span><span>。</span><span>它的意思是，</span><span>wheel</span><span>这个组的所有用户都拥有了</span><span>sudo</span><span>的权利</span><span>。</span><span>接下来就需要你把想让有</span><span>sudo</span><span>权利的所有用户加入到</span><span>wheel</span><span>这个组中即可</span><span>。</span>

<span>![7_34.png.jpg](images/7_34.png.jpg)</span>

