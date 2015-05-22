# 学习 shell 脚本之前的基础知识

<span>日常的</span><span>linux</span><span>系统管理工作中必不可少的就是</span><span>shell</span><span>脚本，如果不会写</span><span>shell</span><span>脚本，那么你就不算一个合格的管理员</span><span>。</span><span>目前很多单位在招聘</span><span>linux</span><span>系统管理员时，</span><span>shell</span><span>脚本的编写是必考的项目</span><span>。</span><span>有的单位甚至用</span><span>shell</span><span>脚本的编写能力来衡量这个</span><span>linux</span><span>系统管理员的经验是否丰富</span><span>。</span><span>笔者讲这些的目的只有一个，那就是让你认真对待</span><span>shell</span><span>脚本，从一开始就要把基础知识掌握牢固，然后要不断的练习，只要你</span><span>shell</span><span>脚本写的好，相信你的</span><span>linux</span><span>求职路就会轻松的多</span><span>。</span><span>笔者在这一章中并不会多么详细的介绍</span><span>shell</span><span>脚本，而只是带你进入</span><span>shell</span><span>脚本的世界，如果你很感兴趣那么请到网上下载相关的资料或者到书店购买相关书籍吧</span><span>。</span>

<span>在学习</span><span>shell</span> <span>脚本之前，需要你了解很多关于</span><span>shell</span><span>的知识，这些知识是编写</span><span>shell</span><span>脚本的基础，所以希望你能够熟练的掌握</span><span>。</span>

<span>**【**</span><span>**什么是**</span><span>**shell】**</span>

<span>简单点理解，就是系统跟计算机硬件交互时使用的中间介质，它只是系统的一个工具</span><span>。</span><span>实际上，在</span><span>shell</span><span>和计算机硬件之间还有一层东西那就是系统内核了</span><span>。</span><span>打个比方，如果把计算机硬件比作一个人的躯体，而系统内核则是人的大脑，至于</span><span>shell</span><span>，把它比作人的五官似乎更加贴切些</span><span>。</span><span>回到计算机上来，用户直接面对的不是计算机硬件而是</span><span>shell</span><span>，用户把指令告诉</span><span>shell</span><span>，然后</span><span>shell</span><span>再传输给系统内核，接着内核再去支配计算机硬件去执行各种操作</span><span>。</span>

<span>笔者接触的</span><span>linux</span><span>发布版本（</span><span>Redhat/CentOS</span><span>）系统默认安装的</span><span>shell</span><span>叫做</span><span>bash</span><span>，即</span><span>Bourne Again Shell</span><span>，它是</span><span>sh</span><span>（</span><span>Bourne Shell</span><span>）的增强版本</span><span>。Bourn Shell</span> <span>是最早行起来的一个</span><span>shell</span><span>，创始人叫</span><span>Steven Bourne</span><span>，为了纪念他所以叫做</span><span>Bourn Shell</span><span>，检称</span><span>sh。</span><span>那么这个</span><span>bash</span><span>有什么特点呢？</span>

<span>1</span><span>）记录命令历史</span>

<span>我们敲过的命令，</span><span>linux</span><span>是会有记录的，预设可以记录</span><span>1000</span><span>条历史命令</span><span>。</span><span>这些命令保存在用户的家目录中的</span><span>.bash_history</span><span>文件中</span><span>。</span><span>有一点需要你知道的是，只有当用户正常退出当前</span><span>shell</span><span>时，在当前</span><span>shell</span><span>中运行的命令才会保存至</span><span>.bash_history</span><span>文件中</span><span>。</span>

<span>与命令历史有关的有一个有意思的字符那就是</span><span>”!”</span><span>了</span><span>。</span><span>常用的有这么几个应用：（</span><span>1</span><span>）</span><span>!!</span> <span>（连续两个</span><span>”!”</span><span>），表示执行上一条指令；（</span><span>2</span><span>）</span><span>!n</span><span>（这里的</span><span>n</span><span>是数字），表示执行命令历史中第</span><span>n</span><span>条指令，例如</span><span>”!100”</span><span>表示执行命令历史中第</span><span>100</span><span>个命令；（</span><span>3</span><span>）</span><span>!</span><span>字符串（字符串大于等于</span><span>1</span><span>），例如</span><span>!ta</span><span>，表示执行命令历史中最近一次以</span><span>ta</span><span>为开头的指令</span><span>。</span>

<span>![12_1.png.jpg](images/12_1.png.jpg)</span>

<span>2</span><span>）指令和文件名补全</span>

<span>在本教程最开始笔者就介绍过这个功能了，记得吗？对了就是按</span><span>tab</span><span>键，它可以帮你补全一个指令，也可以帮你补全一个路径或者一个文件名</span><span>。</span><span>连续按两次</span><span>tab</span><span>键，系统则会把所有的指令或者文件名都列出来</span><span>。</span>

<span>3</span><span>）别名</span>

<span>前面也出现过</span><span>alias</span><span>的介绍，这个就是</span><span>bash</span><span>所特有的功能之一了</span><span>。</span><span>我们可以通过</span><span>alias</span><span>把一个常用的并且很长的指令别名一个简洁易记的指令</span><span>。</span><span>如果不想用了，还可以用</span><span>unalias</span><span>解除别名功能</span><span>。</span><span>直接敲</span><span>alias</span><span>会看到目前系统预设的</span><span>alias</span> <span>：</span>

<span>![12_7.png.jpg](images/12_7.png.jpg)</span><span>

看到了吧，系统预设的</span><span>alias</span><span>指令也就这几个而已，你也可以自定义你想要的指令别名</span><span>。alias</span><span>语法很简单，</span><span>alias [</span><span>命令别名</span><span>]=[’</span><span>具体的命令</span><span>’]。</span>

<span>4</span><span>）通配符</span>

<span>在</span><span>bash</span><span>下，可以使用</span><span>*</span><span>来匹配零个或多个字符，而用</span><span>?</span><span>匹配一个字符</span><span>。</span>

<span>![12_8.png.jpg](images/12_8.png.jpg)</span>

<span>5</span><span>）输入输出从定向</span>

<span>输入重定向用于改变命令的输入，输出重定向用于改变命令的输出</span><span>。</span><span>输出重定向更为常用，它经常用于将命令的结果输入到文件中，而不是屏幕上</span><span>。</span><span>输入重定向的命令是</span><span><</span><span>，输出重定向的命令是</span><span>></span><span>，另外还有错误重定向</span><span>2></span><span>，以及追加重定向</span><span>>></span><span>，稍后会详细介绍</span><span>。</span>

<span>6</span><span>）管道符</span>

<span>前面已经提过过管道符</span><span>”|”</span><span>，就是把前面的命令运行的结果丢给后面的命令</span><span>。</span>

<span>7</span><span>）作业控制</span><span>。</span>

<span>当运行一个进程时，你可以使它暂停（按</span><span>Ctrl+z</span><span>），然后使用</span><span>fg</span><span>命令恢复它，利用</span><span>bg</span><span>命令使他到后台运行，你也可以使它终止（按</span><span>Ctrl+c</span><span>）</span><span>。</span>

<span>**【**</span><span>**变量**</span><span>**】**</span>

<span>前面章节中笔者曾经介绍过环境变量</span><span>PATH</span><span>，这个环境变量就是</span><span>shell</span><span>预设的一个变量，通常</span><span>shell</span><span>预设的变量都是大写的</span><span>。</span><span>变量，说简单点就是使用一个较简单的字符串来替代某些具有特殊意义的设定以及数据</span><span>。</span><span>就拿</span><span>PATH</span><span>来讲，这个</span><span>PATH</span><span>就代替了所有常用命令的绝对路径的设定</span><span>。</span><span>因为有了</span><span>PATH</span><span>这个变量，所以我们运行某个命令时不再去输入全局路径，直接敲命令名即可</span><span>。</span><span>你可以使用</span><span>echo</span><span>命令显示变量的值</span><span>。</span>

<span>![12_9.png.jpg](images/12_9.png.jpg)</span>

<span>除了</span><span>PATH, HOME, LOGNAME</span><span>外，系统预设的环境变量还有哪些呢？</span>

<span>![12_10.png.jpg](images/12_10.png.jpg)</span>

<span>使用</span><span>env</span><span>命令即可全部列出系统预设的全部系统变量了</span><span>。</span><span>不过登录的用户不一样这些环境变量的值也不一样</span><span>。</span><span>当前显示的就是</span><span>root</span><span>这个账户的环境变量了</span><span>。</span><span>下面笔者简单介绍一下常见的环境变量：</span>

<span>PATH</span> <span>决定了</span><span>shell</span><span>将到哪些目录中寻找命令或程序</span>

<span>HOME</span> <span>当前用户主目录</span>

<span>HISTSIZE</span> <span>历史记录数</span>

<span>LOGNAME</span> <span>当前用户的登录名</span>

<span>HOSTNAME</span> <span>指主机的名称</span>

<span>SHELL</span> <span>前用户</span><span>Shell</span><span>类型</span>

<span>LANG</span> <span>语言相关的环境变量，多语言可以修改此环境变量</span>

<span>MAIL</span> <span>当前用户的邮件存放目录</span>

<span>PWD</span> <span>当前目录</span>

<span>env</span><span>命令显示的变量只是环境变量，系统预设的变量其实还有很多，你可以使用</span><span>set</span><span>命令把系统预设的全部变量都显示出来</span><span>。</span>

<span>![12_11.png.jpg](images/12_11.png.jpg)</span>

<span>限于篇幅，笔者在上例中并没有把所有显示结果都截图</span><span>。set</span><span>不仅可以显示系统预设的变量，也可以连同用户自定义的变量显示出来</span><span>。</span><span>用户自定义变量？是的，用户自己同样可以定义变量</span><span>。</span>

<span>![12_21.png.jpg](images/12_21.png.jpg)</span>

<span>虽然你可以自定义变量，但是该变量只能在当前</span><span>shell</span><span>中生效，不信你再登录一个</span><span>shell</span><span>试试？</span>

<span>![12_22.png.jpg](images/12_22.png.jpg)</span>

<span>使用</span><span>bash</span><span>命令即可再打开一个</span><span>shell</span><span>，此时先前设置的</span><span>myname</span><span>变量已经不存在了，退出当前</span><span>shell</span><span>回到原来的</span><span>shell</span><span>，</span><span>myname</span><span>变量还在</span><span>。</span><span>那要想设置的变量一直生效怎么办？有两种情况：</span>

<span>1</span><span>）</span><span>要想系统内所有用户登录后都能使用该变量</span>

<span>需要在</span><span>/etc/profile</span><span>文件最末行加入</span> <span>“export myname=Aming”</span> <span>然后运行</span><span>”source /etc/profile”</span><span>就可以生效了</span><span>。</span><span>此时你再运行</span><span>bash</span><span>命令或者直接</span><span>su - test</span><span>账户看看</span><span>。</span>

<span>![12_23.png.jpg](images/12_23.png.jpg)</span>

<span>2</span><span>）只想让当前用户使用该变量</span>

<span>需要在用户主目录下的</span><span>.bashrc</span><span>文件最后一行加入</span><span>“export myname=Aming”</span> <span>然后运行</span><span>”source .bashrc”</span><span>就可以生效了</span><span>。</span><span>这时候再登录</span><span>test</span><span>账户，</span><span>myname</span><span>变量则不会生效了</span><span>。</span><span>上面用的</span><span>source</span><span>命令的作用是，讲目前设定的配置刷新，即不用注销再登录也能生效</span><span>。</span>

<span>笔者在上例中使用</span><span>”myname=Aming”</span><span>来设置变量</span><span>myname</span><span>，那么在</span><span>linux</span><span>下设置自定义变量有哪些规则呢？</span>

<span>a.</span> <span>设定变量的格式为</span><span>”a=b”</span><span>，其中</span><span>a</span><span>为变量名，</span><span>b</span><span>为变量的内容，等号两边不能有空格；</span>

<span>b.</span> <span>变量名只能由英</span><span>、</span><span>数字以及下划线组成，而且不能以数字开头；</span>

<span>c.</span> <span>当变量内容带有特殊字符（如空格）时，需要加上单引号；</span>

<span>![12_24.png.jpg](images/12_24.png.jpg)</span>

<span>有一种情况，需要你注意，就是变量内容中本身带有单引号，这就需要用到双引号了</span><span>。</span>

<span>![12_25.png.jpg](images/12_25.png.jpg)</span>

<span>d.</span> <span>如果变量内容中需要用到其他命令运行结果则可以使用反引号；</span>

<span>![12_26.png.jpg](images/12_26.png.jpg)</span>

<span>e.</span> <span>变量内容可以累加其他变量的内容，需要加双引号；</span>

<span>![12_27.png.jpg](images/12_27.png.jpg)</span>

<span>在这里如果你不小心把双引号加错为单引号，将得不到你想要的结果</span>

<span>![12_28.png.jpg](images/12_28.png.jpg)</span>

<span>通过上面几个例子也许你能看得出，单引号和双引号的区别：用双引号时不会取消掉里面出现的特殊字符的本身作用（这里的</span><span>$</span><span>），而使用单引号则里面的特殊字符全部失去它本身的作用</span><span>。</span>

<span>在前面的例子中笔者多次使用了</span><span>bash</span><span>命令，如果在当前</span><span>shell</span><span>中运行</span><span>bash</span><span>指令后，则会进入一个新的</span><span>shell</span><span>，这个</span><span>shell</span><span>就是原来</span><span>shell</span><span>的子</span><span>shell</span><span>了，不妨你用</span><span>pstree</span><span>指令来查看一下</span><span>。</span>

<span>![12_29.png.jpg](images/12_29.png.jpg)</span>

pstree<span>这个指令会把</span><span>linux</span><span>系统中所有进程通过树形结构打印出来</span><span>。</span><span>限于篇幅笔者没有全部列出，你可以直接输入</span><span>pstree</span><span>查看即可</span><span>。</span><span>在父</span><span>shell</span><span>中设定一个变量后，进入子</span><span>shell</span><span>后该变量是不会生效的，如果想让这个变量在子</span><span>shell</span><span>中生效则要用到</span><span>export</span><span>指令，笔者曾经在前面用过</span><span>。</span>

<span>![12_44.png.jpg](images/12_44.png.jpg)</span>

export<span>其实就是声明一下这个变量的意思，让该</span><span>shell</span><span>的子</span><span>shell</span><span>也知道变量</span><span>abc</span><span>的值是</span><span>123.</span><span>如果</span><span>export</span><span>后面不加任何变量名，则它会声明所有的变量</span><span>。</span>

<span>![12_45.png.jpg](images/12_45.png.jpg)</span>

<span>在最后面连同我们自定义的变量都被声明了</span><span>。</span>

<span>前面光讲如何设置变量，如果想取消某个变量怎么办？只要输入</span><span>”unset</span> <span>变量名</span><span>”</span><span>即可</span><span>。</span>

<span>![12_46.png.jpg](images/12_46.png.jpg)</span>

<span>用</span><span>unset abc</span><span>后，再</span><span>echo $abc</span><span>则不再输出任何内容</span><span>。</span>

<span>**【**</span><span>**系统环境变量与个人环境变量的配置文件**</span><span>**】**</span>

<span>上面讲了很多系统的变量，那么在</span><span>linux</span><span>系统中，这些变量被存到了哪里呢，为什么用户一登陆</span><span>shell</span><span>就自动有了这些变量呢？</span>

<span>**/etc/profile**</span><span>：这个文件预设了几个重要的变量，例如</span><span>PATH, USER, LOGNAME, MAIL, INPUTRC, HOSTNAME, HISTSIZE, umas</span><span>等等</span><span>。</span>

<span>**/etc/bashrc** </span><span>：这个文件主要预设</span><span>umask</span><span>以及</span><span>PS1。</span><span>这个</span><span>PS1</span><span>就是我们在敲命令时，前面那串字符了，例如笔者的</span><span>linux</span><span>系统</span><span>PS1</span><span>就是</span> <span>[root@localhost ~]#</span> <span>，你不妨看一下</span><span>PS1</span><span>的值</span><span>。</span>

<span>![12_47.png.jpg](images/12_47.png.jpg)</span>

<span>\u</span><span>就是用户，</span><span>\h</span> <span>主机名，</span> <span>\W</span> <span>则是当前目录，</span><span>\$</span><span>就是那个</span><span>’#’</span><span>了，如果是普通用户则显示为</span><span>’$’</span>

<span>除了两个系统级别的配置文件外，每个用户的主目录下还有几个这样的隐藏文件：</span>

<span>**.bash_profile**</span><span>：定义了用户的个人化路径与环境变量的文件名称</span><span>。</span><span>每个用户都可使用该文件输入专用于自己使用的</span><span>shell</span><span>信息</span><span>,</span><span>当用户登录时</span><span>,</span><span>该文件仅仅执行一次</span><span>。</span>

<span>**.bashrc**</span><span>：该文件包含专用于你的</span><span>shell</span><span>的</span><span>bash</span><span>信息</span><span>,</span><span>当登录时以及每次打开新的</span><span>shell</span><span>时</span><span>,</span><span>该该文件被读取</span><span>。</span><span>例如你可以将用户自定义的</span><span>alias</span><span>或者自定义变量写到这个文件中</span><span>。</span>

<span>**.bash_history**</span><span>：记录命令历史用的</span><span>。</span>

<span>**.bash_logout** </span><span>：当退出</span><span>shell</span><span>时，会执行该文件</span><span>。</span><span>可以把一些清理的工作放到这个文件中</span><span>。</span>

<span> </span>

<span>【</span><span>**linux shell**</span><span>**中的特殊符号**</span><span>】</span>

<span>你在学习</span><span>linux</span><span>的过程中，也许你已经接触过某个特殊符号，例如</span><span>”*”</span><span>，它是一个通配符号，代表零个或多个字符或数字</span><span>。</span><span>下面笔者就说一说常用到的特殊字符</span><span>。</span>

<span>**1\. *** </span><span>：代表零个或多个字符或数字</span><span>。</span>

<span>![12_48.png.jpg](images/12_48.png.jpg)</span>

<span>test</span><span>后面可以没有任何字符，也可以有多个字符，总之有或没有都能匹配出来</span><span>。</span>

<span>**2\. ?** </span><span>：只代表一个任意的字符</span>

<span>![12_49.png.jpg](images/12_49.png.jpg)</span>

<span>不管是数字还是字母，只要是一个都能匹配出来</span><span>。</span>

<span>**3\. #** </span><span>：这个符号在</span><span>linux</span><span>中表示注释说明的意思，即</span><span>”#”</span><span>后面的内容</span><span>linux</span><span>忽略掉</span><span>。</span>

<span>![12_50.png.jpg](images/12_50.png.jpg)</span>

<span>在命令的开头或者中间插入</span><span>”#”</span> <span>，</span><span>linux</span><span>都会忽略掉的</span><span>。</span><span>这个符号在</span><span>shell</span><span>脚本中用的很多</span><span>。</span>

<span>**4\. \** </span><span>：脱意字符，将后面的特殊符号（例如</span><span>”*”</span> <span>）还原为普通字符</span><span>。</span>

<span>![12_51.png.jpg](images/12_51.png.jpg)</span>

<span>**5\. |** </span><span>：管道符，前面多次说过，它的作用在于将符号前面命令的结果丢给符号后面的命令</span><span>。</span><span>这里提到的后面的命令，并不是所有的命令都可以的，一般针对文档操作的命令比较常用，例如</span><span>cat, less, head, tail, grep, cut, sort, wc, uniq, tee, tr, split, sed, awk</span><span>等等，其中</span><span>grep, sed, awk</span><span>为正则表达式必须掌握的工具，在后续内容中详细介绍</span><span>。</span>

<span>6\. $</span> <span>：除了用于变量前面的标识符外，还有一个妙用，就是和</span><span>’!’</span><span>结合起来使用</span><span>。</span>

<span>![12_52.png.jpg](images/12_52.png.jpg)</span>

<span>‘!$’</span><span>表示上条命中中最后一个变量（也许称为变量不合适，总之就是上条命令中最后出现的那个东西）例如上边命令最后是</span><span>test.txt</span><span>那么在当前命令下输入</span><span>!$</span><span>则代表</span><span>test.txt。</span>

<span>**1**</span><span>**）**</span><span>**grep**</span><span>：过滤一个或多个字符，将会在后续内容中详细介绍其用法</span><span>。</span>

<span>![12_53.png.jpg](images/12_53.png.jpg)</span>

<span>**2) cut**</span><span>：截取某一个字段</span>

<span>语法：</span><span>cut -d “</span><span>分隔字符</span><span>” [-cf] n</span> <span>这里的</span><span>n</span><span>是数字</span>

<span>-d</span> <span>：后面跟分隔字符，分隔字符要用双引号括起来</span>

<span>-c</span> <span>：后面接的是第几个字符</span>

<span>-f</span> <span>：后面接的是第几个区块</span>

<span>![12_54.png.jpg](images/12_54.png.jpg)</span>

<span>-d</span> <span>后面跟分隔字符，这里使用冒号作为分割字符，</span><span>-f 1</span> <span>就是截取第一段，</span><span>-f</span><span>和</span><span>1</span><span>之间的空格可有可无</span><span>。</span>

<span>![12_55.png.jpg](images/12_55.png.jpg)</span>

<span>-c</span> <span>后面可以是</span><span>1</span><span>个数字</span><span>n</span><span>，也可以是一个区间</span><span>n1-n2</span><span>，还可以是多个数字</span><span>n1,n2,n3</span>

<span>![12_56.png.jpg](images/12_56.png.jpg)</span>

<span>**3) sort**</span><span>：用做排序</span>

<span>语法：</span><span>sort [-t</span> <span>分隔符</span><span>] [-kn1,n2] [-nru]</span> <span>这里的</span><span>n1 < n2</span>

<span>-t</span> <span>分隔符</span><span>：作用跟</span><span>cut</span><span>的</span><span>-d</span><span>一个意思</span>

<span>-n</span> <span>：使用纯数字排序</span>

<span>-r</span> <span>：反向排序</span>

<span>-u</span> <span>：去重复</span>

<span>-kn1,n2</span> <span>：由</span><span>n1</span><span>区间排序到</span><span>n2</span><span>区间，可以只写</span><span>-kn1</span><span>，即对</span><span>n1</span><span>字段排序</span>

<span>![12_57.png.jpg](images/12_57.png.jpg)</span>

<span>![12_78.png.jpg](images/12_78.png.jpg)</span>

<span>![12_79.png.jpg](images/12_79.png.jpg)</span>

<span>**4) wc**</span><span>：统计文档的行数</span><span>、</span><span>字符数</span><span>、</span><span>词数，常用的选项为：</span>

<span>-l</span> <span>：统计行数</span>

<span>-m</span> <span>：统计字符数</span>

<span>-w</span> <span>：统计词数</span>

<span>![12_80.png.jpg](images/12_80.png.jpg)</span>

<span>**5**</span><span>**）**</span><span> **uniq**</span><span>：去重复的行，笔者常用的选项只有一个：</span>

<span>-c</span> <span>：统计重复的行数，并把行数写在前面</span>

<span>![12_81.png.jpg](images/12_81.png.jpg)</span>

<span>有一点需要注意，在进行</span><span>uniq</span><span>之前，需要先用</span><span>sort</span><span>排序然后才能</span><span>uniq</span><span>，否则你将得不到你想要的，笔者上面的试验当中已经是排序过所以省略掉那步了</span><span>。</span>

<span>**6**</span><span>**）**</span><span>**tee** </span><span>：后跟文件名，类似与重定向</span><span>”>”</span><span>，但是比重定向多了一个功能，在把文件写入后面所跟的文件中的同时，还显示在屏幕上</span><span>。</span>

<span>![12_82.png.jpg](images/12_82.png.jpg)</span>

<span>**7**</span><span>**）**</span><span>**tr** </span><span>：替换字符，常用来处理文档中出现的特殊符号，如</span><span>DOS</span><span>文档中出现的</span><span>^M</span><span>符号</span><span>。</span><span>常用的选项有两个：</span>

<span>-d</span> <span>：删除某个字符，</span><span>-d</span> <span>后面跟要删除的字符</span>

<span>-s</span> <span>：把重复的字符去掉</span>

<span>最常用的就是把小写变大写：</span> <span>tr ‘[a-z]’ ‘[A-Z]’</span>

<span>![12_83.png.jpg](images/12_83.png.jpg)</span>

<span>当然替换一个字符也是完全可以的</span><span>。</span>

<span>![12_84.png.jpg](images/12_84.png.jpg)</span>

<span>不过替换</span><span>、</span><span>删除以及去重复都是针对一个字符来讲的，有一定局限性</span><span>。</span><span>如果是针对一个字符串就不再管用了，所以笔者建议只是简单了解这个</span><span>tr</span><span>即可，以后你还会学到更多可以实现针对字符串操作的工具</span><span>。</span>

<span>![12_85.png.jpg](images/12_85.png.jpg)</span>

<span>**8**</span><span>**）**</span><span>**split** </span><span>：切割文档，常用选项：</span>

<span>-b</span> <span>：依据大小来分割文档，单位为</span><span>byte</span>

<span>![12_86.png.jpg](images/12_86.png.jpg)</span>

<span>格式如上例，后面的</span><span>passwd</span><span>为分割后文件名的前缀，分割后的文件名为</span><span>passwdaa, passwdab, passwdac …</span>

<span>-l</span> <span>：依据行数来分割文档</span>

<span>![12_87.png.jpg](images/12_87.png.jpg)</span>

<span>**6\.** </span><span>**；**</span><span>：分号</span><span>。</span><span>平时我们都是在一行中敲一个命令，然后回车就运行了，那么想在一行中运行两个或两个以上的命令如何呢？则需要在命令之间加一个</span><span>”;”</span><span>了</span><span>。</span>

<span>![12_88.png.jpg](images/12_88.png.jpg)</span>

<span>**7\. ~**</span><span>：用户的家目录，如果是</span><span>root</span><span>则是</span> <span>/root</span> <span>，普通用户则是</span> <span>/home/username</span>

<span>![12_89.png.jpg](images/12_89.png.jpg)</span>

<span>**8\. &** </span><span>：如果想把一条命令放到后台执行的话，则需要加上这个符号</span><span>。</span><span>通常用于命令运行时间非常长的情况</span><span>。</span>

<span>![12_90.png.jpg](images/12_90.png.jpg)</span>

<span>使用</span><span>jobs</span><span>可以查看当前</span><span>shell</span><span>中后台执行的任务</span><span>。</span><span>用</span><span>fg</span><span>可以调到前台执行</span><span>。</span><span>这里的</span><span>sleep</span><span>命令就是休眠的意思，后面跟数字，单位为秒，常用语循环的</span><span>shell</span><span>脚本中</span><span>。</span>

<span>![12_91.png.jpg](images/12_91.png.jpg)</span>

<span>此时你按一下</span><span>CTRL +z</span> <span>使之暂停，然后再输入</span><span>bg</span><span>可以再次进入后台执行</span><span>。</span>

<span>![12_92.png.jpg](images/12_92.png.jpg)</span>

<span>如果是多任务情况下，想要把任务调到前台执行的话，</span><span>fg</span><span>后面跟任务号，任务号可以使用</span><span>jobs</span><span>命令得到</span><span>。</span>

<span>![12_93.png.jpg](images/12_93.png.jpg)</span>

<span>9\.</span> <span>**>, >>, 2>, 2>>**</span><span>：前面讲过重定向符号</span><span>></span> <span>以及</span><span>>>　</span><span>分别表示取代和追加的意思，然后还有两个符号就是这里的</span><span>2></span> <span>和</span> <span>2>>　</span><span>分别表示错误重定向和错误追加重定向，当我们运行一个命令报错时，报错信息会输出到当前的屏幕，如果想重定向到一个文本里，则要用</span><span>2></span><span>或者</span><span>2>>。</span>

<span>![12_94.png.jpg](images/12_94.png.jpg)</span>

<span>**10\. [ ]**</span><span>：中括号，中间为字符组合，代表中间字符中的任意一个</span>

<span>![12_95.png.jpg](images/12_95.png.jpg)</span>

<span>**11\. &&** </span><span>**与**</span><span> **||**</span>

<span>在上面刚刚提到了分号，用于多条命令间的分隔符</span><span>。</span><span>另外还有两个可以用于多条命令中间的特殊符号，那就是</span> <span>“&&”</span><span>和</span><span>”||”。</span><span>下面笔者把这几种情况全列出：</span>

<span>1) command1 ; command2</span>

<span>2) command1 && command2</span>

<span>3) command1 || command2</span>

<span>使用</span><span>”;”</span><span>时，不管</span><span>command1</span><span>是否执行成功都会执行</span><span>command2</span><span>；</span><span>使用</span><span>”&&”</span><span>时，只有</span><span>command1</span><span>执行成功后，</span><span>command2</span><span>才会执行，否则</span><span>command2</span><span>不执行；使用</span><span>”||”</span><span>时，</span><span>command1</span><span>执行成功后</span><span>command2</span> <span>不执行，否则去执行</span><span>command2</span><span>，总之</span><span>command1</span><span>和</span><span>command2</span><span>总有一条命令会执行</span><span>。</span>

<span>![12_96.png.jpg](images/12_96.png.jpg)</span>

