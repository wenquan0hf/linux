# Linux 文件与目录管理

<span>在</span><span> linux </span><span>中什么是一个文件的路径呢，说白了就是这个文件存在的地方，例如在上一章提到的</span><span>/root/.ssh/authorized_keys</span> <span>这就是一个文件的路径</span><span>。</span><span>如果你告诉系统这个文件的路径，那么系统就可以找到这个文件</span><span>。</span><span>在</span><span> linux </span><span>的世界中，存在着绝对路径和相对路径</span><span>。</span>

<span>**绝对路径**</span><span>：路径的写法一定由根目录</span><span>”/”</span><span>写起，例如</span><span>/usr/local/mysql</span> <span>这就是绝对路径</span><span>。</span>

<span>**相对路径**</span><span>：路径的写法不是由根目录</span><span>”/”</span><span>写起，例如，首先用户进入到</span><span>/</span> <span>然后再进入到</span><span> home </span> <span>，命令为</span> <span> cd /home </span> <span>然后</span> <span> cd test </span> <span>此时用户所在的路径为</span> <span>/home/test 。</span><span>第一个</span><span>cd</span><span>命令后跟</span> <span> /home </span> <span>第二个</span><span> cd </span><span>命令后跟</span><span> test </span> <span>，并没有斜杠，这个</span><span>test</span><span>是相对于</span><span>/home</span> <span>目录来讲的，所以叫做相对路径</span><span>。</span>

<span>**pwd**</span><span>这个命令打印出当前所在目录</span>

<span>![6_1.png.jpg](images/6_1.png.jpg)</span>

<span>**cd** </span><span>进入到某一个目录</span>

<span>![6_12.png.jpg](images/6_12.png.jpg)</span>

<span>./</span> <span>指的是当前目录</span>

<span>../</span> <span>指的是当前目录的上一级目录</span><span>。</span>

<span>![6_13.png.jpg](images/6_13.png.jpg)</span>

<span>上图中，首先进入到</span><span>/usr/local/lib/</span> <span>目录下，然后再进入</span> <span>./</span> <span>其实还是进入到当前目录下，用</span><span>pwd</span><span>查看当前目录，并没有发生变化，然后再进入</span><span>../</span> <span>则是进入到了</span><span>/usr/local/</span><span>目录下，即</span><span>/usr/local/lib</span><span>目录的上一级目录</span><span>。</span><span>你看明白了吗？</span>

<span>**mkdir**</span><span>创建一个目录，这个命令在上一章节中提及过</span><span>。mkdir</span> <span>其实就是</span><span>make directory</span><span>的缩写</span><span>。</span><span>其语法为</span> <span>mkdir [-mp] [</span><span>目录名称</span><span>]</span> <span>，其中</span><span>-m , –p</span> <span>为其选项，</span><span>-m</span><span>：这个参数用来指定要创建目录的权限，该参数不常用，所以笔者不做重点解释</span><span>。-p</span><span>：这个参数很管用的，先来做个试验，你会一目了然的</span><span>。</span>

<span>![6_14.png.jpg](images/6_14.png.jpg)</span>

<span>当我们想创建</span> <span>/tmp/test/123</span> <span>目录，可是提示不能创建，原因是</span><span>/tmp/test</span><span>目录不存在，你会说，这个</span><span>linux</span><span>怎么这样傻，</span><span>/tmp/test</span><span>目录不存在就自动创建不就</span><span>OK</span><span>了嘛，的确</span><span>linux</span><span>确实很傻，如果它发现要创建的目录的上一级目录不存在就会报错</span><span>。</span><span>然后</span><span>linux</span><span>也为我们想好了解决办法，即</span><span>-p</span><span>参数</span><span>。</span>

<span>![6_15.png.jpg](images/6_15.png.jpg)</span>

<span>你看到这里，是不是明白</span><span>-p</span><span>参数的作用了？没错，它的作用就是递归创建目录，即使上级目录不存在</span><span>。</span><span>还有一种情况就是如果你想要创建的目录存在的话，会提示报错，然后你加上</span><span>-p</span><span>参数后，就不会报错了</span><span>。</span>

<span>![6_16.png.jpg](images/6_16.png.jpg)</span>

<span>**rmdir**</span><span>删除一个目录</span><span>。</span>

<span>![6_17.png.jpg](images/6_17.png.jpg)</span>

<span>rmdir</span> <span>其实是</span><span>rmove directory</span> <span>缩写，其只有一个选项</span><span>-p</span> <span>类似与</span><span>mkdir</span><span>命令，这个参数的作用是将上级目录一起删除</span><span>。</span><span>举个例子吧，新建目录</span><span>mkdir -p d1/d2/d3</span> <span>，</span><span>rmdir -p d1/d2/d3</span><span>相当于是删除了</span><span>d1,d1/d2, d1/d2/d3。</span><span>如果一个目录中还有目录，那么当你直接</span><span>rmdir</span> <span>该目录时，会提示该目录不为空，不能删除</span><span>。</span><span>如果你非要删除不为空的目录，那你用</span><span>rm</span><span>指令吧</span><span>。</span>

<span>**rm**</span><span>删除目录或者文件</span>

<span>rmdir</span> <span>只能删除目录但不能删除文件，要想删除一个文件，则要用</span><span>rm</span><span>命令了</span><span>。rm</span><span>同样也有很多选项</span><span>。</span><span>你可以通过</span> <span>man rm</span> <span>来获得详细帮助信息</span><span>。</span><span>在这里笔者只列举较常用的几个选项</span><span>。</span>

<span>-f</span> <span>强制的意思，如果不加这个选项，当删除一个不存在的文件时会报错</span><span>。</span>

<span>![6_18.png.jpg](images/6_18.png.jpg)</span>

<span>-i</span> <span>这个选项的作用是，当用户删除一个文件时会提示用户是否真的删除</span><span>。</span>

<span>![6_19.png.jpg](images/6_19.png.jpg)</span>

<span>如果删除，输入</span><span>y</span> <span>否则输入</span> <span>n</span>

<span>-r</span> <span>当删除目录时，加该选项，如果不加这个选项会报错</span><span>。rm</span><span>是可以删除不为空的目录的</span><span>。</span>

<span>![6_20.png.jpg](images/6_20.png.jpg)</span>

<span>你会发现，笔者在列举的</span><span>rm</span><span>例子中使用的是绝对路径，而</span><span>ls</span> <span>则使用的相对路径</span><span>。</span><span>这是为什么呢？</span>

<span>![6_21.png.jpg](images/6_21.png.jpg)</span>

<span>**which** </span><span>用来查找一个命令的绝对路径，这个命令笔者不详细介绍，因为平时笔者只用来查找一个命令的绝对路径</span><span>。</span>

<span>**alias**</span><span>用来</span><span>设置指令的别名</span><span>。</span><span>语法：</span><span>alias[</span><span>别名</span><span>]=[</span><span>指令名称</span><span>]</span><span>，例如</span> <span>alias rm='rm -i'</span> <span>，即当我们使用</span><span>rm</span><span>命令时，实际上是使用的是</span><span>rm –i</span> <span>，而用绝对路径的</span><span>/bin/rm</span> <span>则不会被</span><span>alias</span><span>，该命令在以后章节中会详细介绍</span><span>。</span>

## 环境变量 PATH

<span>上边提到了</span><span>alias</span><span>，也提到了绝对路径的</span><span>/bin/rm</span> <span>，然后你意识到没有，为什么我们输入很多命令时是直接打出了命令，而没有去使用这些命令的绝对路径？这是因为环境变量</span><span>PATH</span><span>在起作用了</span><span>。</span><span>请输入</span> <span>echo $PATH</span><span>，这里的</span><span>echo</span><span>其实就是打印的意思，而</span><span>PATH</span><span>前面的</span><span>$</span><span>表示后面接的是变量</span><span>。</span>

<span>![6_65.png.jpg](images/6_65.png.jpg)</span>

<span>因为</span><span>/bin</span> <span>在</span><span>PATH</span><span>的设定中，所以自然就可以找到</span><span>ls</span><span>了</span><span>。</span><span>如果你将</span> <span>ls</span> <span>移动到</span> <span>/root</span> <span>底下的话，然后你自己本身也在</span> <span>/root</span> <span>底下，但是当你执行</span> <span>ls</span> <span>的时候，他就是不理你？怎么办？这是因为</span> <span>PATH</span> <span>没有</span> <span>/root</span> <span>这个目录，而你又将</span> <span>ls</span> <span>移动到</span> <span>/root</span> <span>底下了，自然系统就找不到可执行文件了，因此就会告诉你，</span> <span>command not found</span> <span>！那么该怎么克服这种问题呢？</span>

<span>有两个方法，一种方法是直接将</span> <span>/root</span> <span>的路径加入</span> <span>PATH</span> <span>当中！如何增加？可以使用：</span> <span>　</span>

<span>PATH=”$PATH”:/root</span>

<span>另一种方式则是使用完整档名，亦即直接使用相对或绝对路径来执行，例如：</span>

<span>/root/ls</span>

<span>./ls</span>

<span>关于</span><span>rm</span><span>，笔者使用最多便是</span><span>-rf</span><span>两个选项合用了</span><span>。</span><span>不管删除文件还是目录都可以</span><span>。</span><span>但是方便的同时也要多注意，万一你的手太快后边跟了</span><span>/</span><span>那样就会把你的系统文件全部删除的，切记切记</span><span>。</span>

<span>![6_66.png.jpg](images/6_66.png.jpg)</span>

<span>**ls** </span><span>在前面的命令中多次用到它</span><span>。</span><span>现在你已经明白它的含义了吧</span><span>。</span><span>没有错，就是查看某个目录或者某个文件，是</span><span>list</span><span>的简写</span><span>。ls</span> <span>后可以跟一个目录，也可以跟一个文件</span><span>。</span><span>以下是</span><span>ls</span><span>的选项，在这里笔者并没有完全列出，只是列出了平时使用最多的选项</span><span>。</span><span>其他选项，你可以自行通过</span><span>man ls</span> <span>查询</span><span>。</span>

<span>-a</span> <span>全部的档案都列出，包括隐藏的</span><span>。linux</span><span>文件系统中同样也有隐藏文件</span><span>。</span><span>这些隐藏文件的文件名是以</span><span>.</span><span>开头的</span><span>。</span><span>例如</span><span>.test, /root/.123, /root/.ssh</span> <span>等等，隐藏文件可以是目录也可以是普通文件</span><span>。</span>

<span>-l</span> <span>详细列出文件的属性信息，包括大小</span><span>、</span><span>创建日期</span><span>、</span><span>所属主所属组等等</span><span>。ll</span> <span>这个命令等同于</span><span>ls –l 。</span>

<span>![6_67.png.jpg](images/6_67.png.jpg)</span>

<span>--color=never/always/auto never</span><span>即不要显示颜色，</span><span>always</span> <span>即总显示颜色，</span><span>auto</span> <span>是由系统自行判断</span><span>。</span><span>在</span><span>Redhat/CentOS</span> <span>系统中，默认是带颜色的，因为我们平时用的</span><span>ls</span><span>已经</span><span>alias</span><span>成了</span><span>ls –color=tty</span> <span>所以目录的颜色是蓝色的，而可执行文件的颜色是绿色</span><span>。</span><span>这样有助于帮我们区分文件的格式</span><span>。</span>

<span>![6_68.png.jpg](images/6_68.png.jpg)</span>

<span>-d</span> <span>后边跟目录，如果不加这个选项则列出目录下的文件，加上后只列车目录本身</span><span>。</span>

<span>![6_69.png.jpg](images/6_69.png.jpg)</span>

<span>**cp**</span> <span>copy</span><span>的简写，即拷贝</span><span>。</span><span>格式为</span> <span>cp [</span><span>选项</span><span>] [</span> <span>来源文件</span> <span>] [</span><span>目的文件</span><span>]</span> <span>，例如我想把</span><span>test1</span> <span>拷贝成</span><span>test2</span> <span>，这样即可</span> <span>cp test1 test2</span><span>，以下介绍几个常用的选项</span>

<span>-d</span> <span>这里涉及到一个</span><span>“</span><span>连接</span><span>”</span><span>的概念</span><span>。</span><span>连接分为软连接和硬连接</span><span>。</span><span>在以后的章节中会详细解释，现在你只要明白这里的软连接跟</span><span>windows</span><span>中的快捷方式类似即可</span><span>。</span><span>如果不加这个</span><span>-d</span> <span>则拷贝软连接时会把软连接的目标文件拷贝过去，而加上后，其实只是拷贝了一个连接文件（即快捷方式）</span><span>。</span>

<span>![6_70.png.jpg](images/6_70.png.jpg)</span>

<span>上例中的</span><span>ln</span> <span>命令即为建立连接的，以后再做详细解释</span><span>。</span>

<span>-r</span> <span>如果你要拷贝一个目录，必须要加</span><span>-r</span><span>选项，否则你是拷贝不了目录的</span><span>。</span>

<span>![6_71.png.jpg](images/6_71.png.jpg)</span>

<span>-i</span> <span>如果遇到一个存在的文件，会问是否覆盖</span><span>。</span><span>在</span><span>Redhat/CentOS</span><span>系统中，我们使用的</span><span>cp</span><span>其实是</span><span>cp –i</span>

<span>![6_72.png.jpg](images/6_72.png.jpg)</span>

<span>下面简单做一个小试验，很快你就会明白</span><span>-i</span> <span>选项的作用了</span><span>。</span>

<span>![6_73.png.jpg](images/6_73.png.jpg)</span>

<span>上例中，</span><span>touch</span> <span>命令，看字面意思就是摸一下，没错，如果有这个文件，则会改变文件的访问时间，如果没有这个文件就会创建这个文件</span><span>。</span><span>前面说过</span><span>echo</span><span>，其实就是打印，在这里所</span><span>echo</span><span>的内容</span><span>”abc”</span> <span>和</span> <span>“def”</span><span>并没有显示在屏幕上，而是分别写进了文件</span> <span>111</span><span>和</span><span>222,</span> <span>其写入作用的就是这个大于号</span><span>”>”</span> <span>在</span><span>linux</span><span>中这叫做重定向，即把前面产生的输出写入到后面的文件中</span><span>。</span><span>在以后的章节中会做详细介绍，这里你要明白它的含义即可</span><span>。</span><span>而</span><span>cat</span> <span>命令则是读一个文件，并把读出的内容打印到当前屏幕上</span><span>。</span><span>该命令也会在后续章节中详细介绍</span><span>。</span>

<span>-u</span> <span>该选项仅当目标文件存在时才会生效，如果源文件比目标文件新才会拷贝，否则不做任何动作</span><span>。</span>

<span>**mv** </span><span>移动的意思，是</span><span>move</span><span>的简写</span><span>。</span><span>格式为</span> <span>mv [</span> <span>选项</span> <span>] [</span><span>源文件</span><span>] [</span><span>目标文件</span><span>]</span><span>，下面介绍几个常用的选项</span><span>。</span>

<span>-i</span> <span>和</span><span>cp</span><span>的</span><span>-i</span> <span>一样，当目标文件存在时会问用户是否要覆盖</span><span>。</span><span>在</span><span>Redhat/CentOS</span><span>系统中，我们使用的</span><span>mv</span><span>其实是</span><span>mv –i</span>

<span>-u</span> <span>和上边</span><span>cp</span> <span>命令的</span><span>-u</span><span>选项一个作用，当目标文件存在时才会生效，如果源文件比目标文件新才会移动，否则不做任何动作</span><span>。</span>

<span>该命令有集中情况，你注意到了吗？</span>

<span>1</span><span>）</span><span>目标文件是目录，而且目标文件不存在；</span>

<span>2</span><span>）</span><span>目标文件是目录，而且目标文件存在；</span>

<span>3</span><span>）</span><span>目标文件不是目录不存在；</span>

<span>4</span><span>）</span><span>目标文件不是目录存在；</span>

<span>目标文件是目录，存在和不存在，移动的结果是不一样的，如果存在，则会把源文件移动到目标文件目录中</span><span>。</span><span>不存在的话移动完后，目标文件是一个文件</span><span>。</span><span>这样说也许你会觉得有点不好理解，看例子吧</span><span>。</span>

<span>![6_74.png.jpg](images/6_74.png.jpg)</span>

<span>windows</span><span>下的重命名，在</span><span>linux</span><span>下用</span><span>mv</span><span>就可以搞定</span><span>。</span>

<span>**cat** </span><span>比较常用的一个命令，即查看一个文件的内容并显示在屏幕上</span><span>。</span>

<span>-n</span> <span>查看文件时，把行号也显示到屏幕上</span><span>。</span>

<span>![6_75.png.jpg](images/6_75.png.jpg)</span>

<span>上例中出现了一个</span><span>”>>”</span><span>，这个符号跟前面介绍的</span><span>”>”</span><span>的作用都是重定向，即把前面输出的东西输入到后边的文件中，只是</span><span>”>>”</span><span>是追加的意思，而用</span><span>”>”</span><span>，如果文件中有内容则会删除文件中内容，而</span><span>”>>”</span><span>则不会</span><span>。</span>

<span>-A</span> <span>显示所有东西出来，包括特殊字符</span>

<span>![6_76.png.jpg](images/6_76.png.jpg)</span>

<span>**tac**</span><span>其实是</span><span>cat</span><span>的反写，同样的功能也是反向打印文件的内容到屏幕上</span><span>。</span>

<span>![6_77.png.jpg](images/6_77.png.jpg)</span>

<span>**more**</span><span>也是用来查看一个文件的内容</span><span>。</span><span>当文件内容太多，一屏幕不能占下，而你用</span><span>cat</span><span>肯定是看不前面的内容的，那么使用</span><span>more</span><span>就可以解决这个问题了</span><span>。</span><span>当看完一屏后按空格键继续看下一屏</span><span>。</span><span>但看完所有内容后就会退出</span><span>。</span><span>如果你想提前退出，只需按</span><span>q</span><span>键即可</span><span>。</span>

<span>**less**</span><span>作用跟</span><span>more</span><span>一样，但比</span><span>more</span><span>好在可以上翻，下翻</span><span>。</span><span>空格键同样可以翻页，而按</span><span>”j”</span><span>键可以向下移动（按一下就向下移动一行），按</span><span>”k”</span><span>键向上移动</span><span>。</span><span>在使用</span><span>more</span><span>和</span><span>less</span><span>查看某个文件时，你可以按一下</span><span>”/”</span> <span>键，然后输入一个</span><span>word</span><span>回车，这样就可以查找这个</span><span>word</span><span>了</span><span>。</span><span>如果是多个该</span><span>word</span><span>可以按</span><span>”n”</span><span>键显示下一个</span><span>。</span><span>另外你也可以不按</span><span>”/”</span><span>而是按</span><span>”?”</span><span>后边同样跟</span><span>word</span><span>来搜索这个</span><span>word</span><span>，唯一不同的是，</span><span>”/”</span><span>是在当前行向下搜索，而</span><span>”?”</span><span>是在当前行向上搜索</span><span>。</span>

<span>**head**</span> <span>head</span><span>后直接跟文件名，则显示文件的前十行</span><span>。</span><span>如果加</span> <span>–n</span> <span>选项则显示文件前</span><span>n</span><span>行</span><span>。</span>

<span>![6_78.png.jpg](images/6_78.png.jpg)</span>

<span>**tail** </span><span>和</span><span>head</span><span>一样，后面直接跟文件名，则显示文件最后十行</span><span>。</span><span>如果加</span><span>-n</span> <span>选项则显示文件最后</span><span>n</span><span>行</span><span>。</span>

<span>![6_79.png.jpg](images/6_79.png.jpg)</span>

<span>-f</span> <span>动态显示文件的最后十行，如果文件是不断增加的，则用</span><span>-f</span> <span>选项</span><span>。</span><span>如：</span><span>tail -f /var/log/messages</span>

## 文件的所属主以及所属组

<span>一个</span><span>linux</span><span>目录或者文件，都会有一个所属主和所属组</span><span>。</span><span>所属主，即文件的拥有者，而所属组，即该文件所属主所在的一个组</span><span>。Linux</span><span>这样设置文件属性的目的是为了文件的安全</span><span>。</span><span>例如，</span><span>test</span><span>文件的所属主是</span><span>user0</span> <span>而</span><span>test1</span><span>文件的所属主是</span><span>user1</span><span>，那么</span><span>user1</span><span>是不能查看</span><span>test</span><span>文件的，相应的</span><span>user0</span><span>也不能查看</span><span>test1</span><span>文件</span><span>。</span><span>然后有这样一个应用，我想创建一个文件同时让</span><span>user0</span><span>和</span><span>user1</span><span>来查看怎么办呢？</span>

<span>这时</span><span>“</span><span>所属组</span><span>”</span><span>就派上用场了</span><span>。</span><span>即，创建一个群组</span><span>users</span><span>，让</span><span>user0</span><span>和</span><span>user1</span><span>同属于</span><span>users</span><span>组，然后建立一个文件</span><span>test2</span><span>，且其所属组为</span><span>users</span><span>，那么</span><span>user0</span><span>和</span><span>user1</span><span>都可以访问</span><span>test2</span><span>文件</span><span>。</span>

<span>Linux</span><span>文件属性不仅规定了所属主和所属组，还规定了所属主（</span><span>user</span><span>）</span><span>、</span><span>所属组</span><span>(group)</span><span>以及其他用户（</span><span>others</span><span>）对该文件的权限</span><span>。</span><span>你可以通过</span><span>ls -l</span> <span>来查看这些属性</span><span>。</span>

<span>![6_80.png.jpg](images/6_80.png.jpg)</span>

## linux 文件属性

<span>上例中，用</span><span>ls –l</span> <span>查看当前目录下的文件时，共显示了</span><span>9</span><span>列内容（用空格划分列），都代表了什么含义呢？</span>

<span>第</span><span>1</span><span>列，包含的东西有该文件类型和所属主</span><span>、</span><span>所属组以及其他用户对该文件的权限</span><span>。</span><span>第一列共</span><span>10</span><span>位</span><span>。</span><span>其中第一位用来描述该文件的类型</span><span>。</span><span>上例中，我们看到的类型有</span><span>”d”, “-“</span> <span>，其实除了这两种外还有</span><span>”l”, “b”, “c”,”s”</span><span>等</span><span>。</span>

<span>d</span> <span>表示该文件为目录；</span>

<span>-</span> <span>表示该文件为普通文件；</span>

<span>l</span> <span>表示该文件为连接文件（</span><span>linux file</span><span>），上边提到的软连接即为该类型；</span>

<span>![6_81.png.jpg](images/6_81.png.jpg)</span>

<span>b</span> <span>表示该文件为块设备文件，比如磁盘分区</span>

<span>![6_82.png.jpg](images/6_82.png.jpg)</span>

<span>c</span> <span>表示该文件为串行端口设备，例如键盘</span><span>、</span><span>鼠标</span><span>。</span>

<span>s</span> <span>表示该文件为套接字文件（</span><span>socket</span><span>），用于进程间通信</span><span>。</span>

<span>后边的</span><span>9</span><span>位，每三个为一组</span><span>。</span><span>均为</span><span>rwx</span> <span>三个参数的组合</span><span>。</span><span>其中</span><span>r</span> <span>代表可读，</span><span>w</span><span>代表可写，</span><span>x</span><span>代表可执行</span><span>。</span><span>前三位为所属主（</span><span>user</span><span>）的权限，中间三位为所属组（</span><span>group</span><span>）的权限，最后三位为其他非本群组（</span><span>others</span><span>）的权限</span><span>。</span><span>下面拿一个具体的例子来述说一下</span><span>。</span>

<span>一个文件的属性为</span><span>-rwxr-xr--</span> <span>，它代表的意思是，该文件为普通文件，文件拥有者可读可写可执行，文件所属组对其可读不可写可执行，其他用户对其只可读</span><span>。</span>

<span>对于一个目录来讲，打开这个目录即为执行这个目录，所以任何一个目录必须要有</span><span>x</span><span>权限才能打开并查看该目录</span><span>。</span><span>例如一个目录的属性为</span> <span>drwxr--r--</span> <span>其所属主为</span><span>root</span><span>，那么除了</span><span>root</span><span>外的其他用户是不能打开这个目录的</span><span>。</span>

<span>第</span><span>2</span><span>列，表示为连接占用的节点（</span><span>inode</span><span>），若为目录时，通常与该目录地下还有多少目录有关系，关于连接（</span><span>link</span><span>）在以后章节详细介绍</span><span>。</span>

<span>第</span><span>3</span><span>列，表示该文件的所属主</span><span>。</span>

<span>第</span><span>4</span><span>列，表示该文件的所属组</span><span>。</span>

<span>第</span><span>5</span><span>列，表示该文件的大小</span><span>。</span>

<span>第</span><span>6</span><span>列</span><span>、</span><span>第</span><span>7</span><span>列和第</span><span>8</span><span>列为该文件的创建日期或者最近的修改日期，分别为月份日期以及时间</span><span>。</span>

<span>第</span><span>9</span><span>列，文件名</span><span>。</span><span>如果前面有一个</span><span>.</span> <span>则表示该文件为隐藏文件</span><span>。</span>

## 更改文件的权限

<span>更改文件的权限，也就是更改所属主</span><span>、</span><span>所属组以及他们对应的读写执行权限</span><span>。</span>

<span>1</span><span>）</span><span>**更改所属组**</span><span> **chgrp**</span>

<span>语法：</span><span>chgrp [</span><span>组名</span><span>] [</span><span>文件名</span><span>]</span>

<span> </span>

<span>![6_83.png.jpg](images/6_83.png.jpg)</span>

<span>这里用到了</span><span>groupadd</span> <span>命令，其含义即增加一个用户组</span><span>。</span><span>该命令在以后章节中做详细介绍，你只要知道它是用来增加用户组的即可</span><span>。</span>

<span>2</span><span>）</span><span>**更改文件的所属主**</span><span> **chown**</span>

<span>语法：</span><span>chown [ -R ]</span> <span>账户名</span><span>文件名</span>

<span>chown [ -R ]</span> <span>账户名：组名</span><span>文件名</span>

<span>这里的</span><span>-R</span><span>选项只作用于目录，作用是级联更改，即不仅更改当前目录，连目录里的目录或者文件全部更改</span><span>。</span>

<span>![6_84.png.jpg](images/6_84.png.jpg)</span>

<span>useradd</span> <span>是增加一个账户，以后会详细介绍</span><span>。</span><span>上例中，首先建立一个目录</span><span>test</span><span>，然后在</span><span>test</span><span>目录下创建一个普通文件</span><span>test2</span><span>，因为是以</span><span>root</span><span>的身份创建的目录和文件，所以所属主以及所属组都是</span><span>root。chown user1 test</span> <span>这使</span><span>test</span><span>的目录所属主由</span><span>root</span><span>变为了</span><span>user1</span> <span>，然后</span><span>test</span><span>目录下的</span><span>test2</span><span>文件所属主以及所属组还是</span><span>root。</span><span>接着</span> <span>chown –R user1:testgroup test</span> <span>这样把</span><span>test</span><span>连同</span><span>test</span><span>目录下的</span><span>test2</span> <span>的所属主以及所属组都改变了</span><span>。</span>

<span>3</span><span>）</span><span>**改变用户对文件的读写执行权限**</span><span> **chmod**</span>

<span>在</span><span>linux</span><span>中为了方便更改这些权限，</span><span>linux</span><span>使用数字去代替</span><span>rwx</span> <span>，具体规则为</span><span>r: 4 w:2 x:1 -:0</span> <span>举个例子，</span><span>-rwxrwx---</span><span>用数字表示就是</span> <span>770</span><span>，具体是这样来的：</span>

<span>rwx = 4+2+1=7; rwx= 4+2+1=7; --- = 0+0+0=0</span>

<span>chmod</span> <span>语法：</span> <span>chmod [-R] xyz</span> <span>文件名</span><span>（这里的</span><span>xyz</span><span>，表示数字）</span>

<span>-R</span> <span>选项作用同</span><span>chown</span><span>，级联更改</span><span>。</span>

<span>值得提一下的是，在</span><span>linux</span><span>系统中，默认一个目录的权限为</span> <span>755</span><span>，而一个文件的默认权限为</span><span>644.</span>

<span>![6_85.png.jpg](images/6_85.png.jpg)</span>

<span>如果你创建了一个目录，而该目录不想让其他人看到内容，则只需设置成</span> <span>rwxr----- (740)</span> <span>即可</span><span>。</span>

<span>chmod</span> <span>还支持使用</span><span>rwx</span><span>的方式来设置权限</span><span>。</span><span>！从之前的介绍中我们可以发现，基本上就九个属性分别是</span><span>(1)user (2)group (3)others</span> <span>三群啦！那么我们就可以藉由</span> <span>u, g, o</span> <span>来代表三群的属性！此外，</span> <span>a</span> <span>则代表</span> <span>all</span> <span>亦即全部的三群！那么读写的属性就可以写成了</span> <span>r, w, x</span><span>！也就是可以使用底下的方式来看：</span>

<span>![6_86.png.jpg](images/6_86.png.jpg)</span>

<span>现在我想把一个文件设置成这样的权限</span> <span>rwxr-xr-x (755)</span><span>，使用这种方式改变权限的命令为</span>

<span>![6_87.png.jpg](images/6_87.png.jpg)</span>

<span>另外还可以针对</span><span>u, g, o, a</span><span>增加或者减少某个权限（读，写，执行），例如</span>

<span>![6_88.png.jpg](images/6_88.png.jpg)</span>

<span>另外linux下还有两个比较特殊的权限s和t，请点击<a>linux下文件的特殊权限s和t</a></span>

<span>**umask**</span>

<span>上边也提到了默认情况下，目录权限值为</span><span>766</span><span>，普通文件权限值为</span><span>644。</span><span>那么这个值是由谁规定呢？追究其原因就涉及到了</span><span>umask。</span>

<span>umask</span><span>语法：</span> <span>umask xxx</span> <span>（这里的</span><span>xxx</span><span>代表三个数字）</span>

<span>查看</span><span>umask</span><span>值只要输入</span><span>umask</span><span>然后回车</span><span>。 umask</span><span>预设是</span><span>0022</span><span>，其代表什么含义？先看一下下面的规则：</span>

<span>1</span><span>）若用户建立为普通文件，则预设</span><span>“</span><span>没有可执行权限</span><span>”</span><span>，只有</span><span>rw</span><span>两个权限</span><span>。</span><span>最大为</span><span>666</span><span>（</span><span>-rw-rw-rw-</span><span>）</span>

<span>2</span><span>）若用户建立为目录，则预设所有权限均开放，即</span><span>777</span><span>（</span><span>drwxrwxrwx</span><span>）</span>

<span>umask</span><span>数值代表的含义为，上边两条规则中的</span><span>默认值（文件为</span><span>666</span><span>，目录为</span><span>777</span><span>）需要减掉的权限</span><span>。</span><span>所以目录的权限为</span><span>(rwxrwxrwx) – (----w--w-) = (rwxr-xr-x)</span><span>，普通文件的权限为</span><span>(rw-rw-rw-) – (----w--w-) = (rw-r--r--)。umask</span><span>的值是可以自定义的，比如设定</span><span>umask</span> <span>为</span> <span>002</span><span>，你再创建目录或者文件时，默认权限分别为</span><span>(rwxrwxrwx) – (-------w-) = (rwxrwxr-x)</span><span>和</span><span>(rw-rw-rw-) – (-------w-) = (rw-rw-r--)。</span>

<span>![6_89.png.jpg](images/6_89.png.jpg)</span>

<span>umask</span> <span>可以在</span><span>/etc/bashrc</span><span>里面更改，预设情况下，</span><span>root</span><span>的</span><span>umask</span><span>为</span><span>022</span><span>，而一般使用者则为</span><span>002</span><span>，因为可写的权限非常重要，因此预设会去掉写权限</span><span>。</span>

<span>**chattr** </span><span>**修改文件的特殊属性**</span>

<span>语法：</span> <span>chattr [+-=][ASaci [</span><span>文件或者目录名</span><span>]</span>

<span>+-=</span> <span>：分别为增加</span><span>、</span><span>减少</span><span>、</span><span>设定</span>

<span>A</span><span>：增加该属性后，文件或目录的</span><span>atime</span><span>将不可被修改；</span>

<span>S</span><span>：增加该属性后，会将数据同步写入磁盘中；</span>

<span>a</span><span>：增加该属性后，只能追加不能删除，非</span><span>root</span><span>用户不能设定该属性；</span>

<span>c</span><span>：自动压缩该文件，读取时会自动解压；</span>

<span>i</span><span>：增加后，使文件不能被删除</span><span>、</span><span>重命名</span><span>、</span><span>设定连接</span><span>、</span><span>写入</span><span>、</span><span>新增数据；</span>

<span>![6_90.png.jpg](images/6_90.png.jpg)</span>

<span>增加</span><span>i</span><span>属性后不能在该目录中建立文件</span><span>。</span>

<span>![6_91.png.jpg](images/6_91.png.jpg)</span>

<span>增加</span><span>a</span><span>属性后，只能追加不能删除</span><span>。</span>

<span>**lsattr** </span><span>**列出文件**</span><span>**/**</span><span>**目录的特殊属性**</span>

<span>语法：</span> <span>lsattr [-aR] [</span><span>文件</span><span>/</span><span>目录名</span><span>]</span>

<span>-a</span><span>：类似与</span><span>ls</span> <span>的</span><span>-a</span> <span>选项，即连同隐藏文件一同列出；</span>

<span>-R</span><span>：连同子目录的数据一同列出</span>

<span>![6_92.png.jpg](images/6_92.png.jpg)</span>

<span>在上例中，</span><span>test4</span><span>是在</span><span>test3</span><span>目录增加</span><span>a</span><span>属性后建立的，所以</span><span>test4</span><span>也有</span><span>a</span><span>属性，通过这个例子可以看出，</span><span>chattr</span> <span>的属性是级联生效的，不仅对当前目录生效而且会对目录下的文件同样生效</span><span>。</span>

## 在 linux 下搜索一个文件

<span>在</span><span>windows</span><span>下有一个搜索工具，可以让我们很快的找到一个文件，这是很有用的</span><span>。</span><span>然而在</span><span>linux</span><span>下搜索功能更加强大</span><span>。</span>

<span>**which**</span><span>用来查找可执行文件的绝对路径</span><span>。</span>

<span>在前面章节中已经多次用到该命令，需要注意的一点是，</span><span>which</span><span>只能用来查找</span><span>PATH</span><span>环境变量中出现的路径下的可执行文件</span><span>。</span><span>这个命令用的也是蛮多的，有时候我们不知道某个命令的绝对路径，</span><span>which</span><span>一下很容易就知道了</span><span>。</span>

<span>![6_93.png.jpg](images/6_93.png.jpg)</span>

<span>当查找的文件在</span><span>PATH</span><span>变量中并没有时，就会报错</span><span>。</span>

<span>**whereis** </span><span>通过预先生成的一个文件列表库去查找跟给出的文件名相关的文件</span><span>。</span>

<span>语法：</span> <span>whereis [-bmsu] [</span><span>文件名称</span><span>]</span>

<span>-b</span><span>：只找</span><span>binary</span> <span>文件</span>

<span>-m</span><span>：只找在说明文件</span><span>manual</span><span>路径下的文件</span>

<span>-s</span><span>：只找</span><span>source</span><span>来源文件</span>

<span>-u</span><span>：没有说明档的文件</span>

<span>![6_94.png.jpg](images/6_94.png.jpg)</span>

<span>说明：</span><span>whereis</span> <span>笔者几乎很少用到，如果你感兴趣请深入研究</span><span>。</span>

<span>**locate**</span><span>类似于</span><span>whereis</span><span>，也是通过查找预先生成的文件列表库来告诉用户要查找的文件在哪里</span><span>。</span><span>后边直接跟文件名</span><span>。</span><span>如果你的</span><span>linux</span><span>没有这个命令，请安装软件包</span> <span>mlocate</span> <span>，这个软件包在你的系统安装盘里，后缀名是</span><span>RPM</span><span>，随后介绍的</span><span>find</span><span>命令会告诉你如何查找这个包</span><span>。</span><span>如果你装的</span><span>CentOS</span><span>你可以使用这个命令来安装</span> <span>yum install –y mlocate 。</span> <span>前提是你的</span><span>CentOS</span><span>能连互联网</span><span>。</span><span>至于</span><span>yum</span><span>这个命令如何使用，到后续章节你自然会明白</span><span>。</span><span>如果你刚装上这个命令，初次使用会报错</span><span>。</span>

<span>![6_95.png.jpg](images/6_95.png.jpg)</span>

<span>这是因为系统还没有生成那个文件列表库</span><span>。</span><span>你可以使用</span><span>updatedb</span> <span>命令立即生成（更新）这个库</span><span>。</span><span>如果你的服务器上正跑着重要的业务，那么你最好不要去运行这个命令，因为一旦运行，服务器的压力会变大</span><span>。</span><span>这个数据库默认情况下每周更新一次</span><span>。</span><span>所以你用</span><span>locate</span><span>命令去搜索一个文件，正好是在两次更新时间段内，那你肯定是得不到结果的</span><span>。</span><span>你可以到</span><span>/etc/updated.conf</span> <span>去配置这个数据库生成（更新）的规则</span><span>。locate</span><span>命令笔者用的也并不多，所以你只要明白有这么一个东西即可</span><span>。</span><span>你用到时再去深究其用法吧</span><span>。</span>

<span>**find** </span><span>这个搜索工具是笔者用的最多的一个，所以请你务必要熟悉它</span><span>。</span>

<span>语法：</span> <span>find [</span><span>路径</span><span>] [</span><span>参数</span><span>]</span> <span>下面介绍几个笔者经常用的参数</span>

<span>-atime +n</span> <span>：访问或执行时间大于</span><span>n</span><span>天的文件</span>

<span>-ctime +n</span> <span>：写入</span><span>、</span><span>更改</span><span>inode</span><span>属性（例如更改所有者</span><span>、</span><span>权限或者连接）时间大于</span><span>n</span><span>天的文件</span>

<span>-mtime +n</span> <span>：写入时间大于</span><span>n</span><span>天的文件</span>

<span>看到这里，你对这三个</span><span>time</span><span>是不是有些晕了，那笔者就先给你介绍一下这三个</span><span>time</span><span>属性</span><span>。</span>

<span>文件的</span> <span>Access time</span><span>，</span><span>atime</span> <span>是在读取文件或者执行文件时更改的</span><span>。</span><span>文件的</span> <span>Modified time</span><span>，</span><span>mtime</span> <span>是在写入文件时随文件内容的更改而更改的</span><span>。</span><span>文件的</span> <span>Create time</span><span>，</span><span>ctime</span> <span>是在写入文件</span><span>、</span><span>更改所有者</span><span>、</span><span>权限</span><span>或链接</span><span>设置</span><span>时随</span> <span>Inode</span> <span>的内容更改而更改的</span><span>。</span> <span>因此，更改文件的内容即会更改</span> <span>mtime</span> <span>和</span> <span>ctime</span><span>，但是文件的</span> <span>ctime</span> <span>可能会在</span> <span>mtime</span> <span>未发生任何变化时更改，例如，更改了文件的权限，但是文件内容没有变化</span><span>。</span> <span>如何获得一个文件的</span><span>atime mtime</span> <span>以及</span><span>ctime</span> <span>？</span>

<span>ls -l</span> <span>命令可用来列出文件的</span> <span>atime、ctime</span> <span>和</span> <span>mtime。</span>

<span>ls -lc filename         </span><span>列出文件的</span> <span>ctime</span>

<span>ls -lu filename         </span><span>列出文件的</span> <span>atime</span>

<span>ls -l filename         </span> <span>列出文件的</span> <span>mtime    </span>

<span>atime</span><span>不一定在</span><span>访问</span><span>文件之后被修改，因为：使用</span><span>ext3</span><span>文件</span><span>系统</span><span>的时候，如果在</span><span>mount</span><span>的时候使用了</span><span>noatime</span><span>参数那么就不会更新</span><span>atime</span><span>的信息</span><span>。</span><span>而这是加了</span> <span>noatime</span> <span>取消了</span><span>,</span> <span>不代表真实情況</span><span>。</span><span>反正</span><span>,</span> <span>這三個</span> <span>time stamp</span> <span>都放在</span> <span>inode</span> <span>中</span><span>。</span><span>若</span> <span>mtime, atime</span> <span>修改</span><span>inode</span> <span>就一定會改</span><span>,</span> <span>既然</span> <span>inode</span> <span>改了</span><span>,</span> <span>那</span> <span>ctime</span> <span>也就跟著要改了</span><span>。</span>

<span>继续讲</span><span>find</span><span>常用的参数</span><span>。</span>

<span>-name filename</span> <span>直接查找该文件名的文件，这个使用最多了</span><span>。</span>

<span>![6_96.png.jpg](images/6_96.png.jpg)</span>

<span>-type type</span> <span>：通过文件类型查找</span><span>。</span><span>文件类型在前面部分已经简单介绍过，相信你已经大体上了解了</span><span>。type</span> <span>包含了</span> <span>f, b, c, d, l, s</span> <span>等等</span><span>。</span><span>后续的内容还会介绍文件类型的</span><span>。</span>

<span>![6_97.png.jpg](images/6_97.png.jpg)</span>

## linux 的文件系统

<span>搞计算机的应该都知道</span><span>windows</span><span>的系统格式化硬盘时会指定格式，</span><span>fat</span> <span>或者</span> <span>ntfs。</span><span>而</span><span>linux</span><span>的文件系统格式为</span><span>Ext2</span><span>，或者</span><span>Ext3 。</span><span>早期的</span><span>linux</span><span>使用</span><span>Ext2</span><span>格式，目前的</span><span>linux</span><span>都使用了</span><span>Ext3。 Ext2</span><span>文件系统虽然是高效稳定的</span><span>。</span><span>但是，随着</span><span>Linux</span><span>系统在关键业务中的应用，</span><span>Linux</span><span>文件系统的弱点也渐渐显露出来了，因为</span><span>Ext2</span><span>文件系统是非日志文件系统</span><span>。</span><span>这在关键行业的应用是一个致命的弱点</span><span>。Ext3</span><span>文件系统是直接从</span><span>Ext2</span><span>文件系统发展而来，</span><span>Ext3</span><span>文件系统带有日志功能，可以跟踪记录文件系统的变化，并将变化内容写入日志，写操作首先是对日志记录文件进行操作，若整个写操作由于某种原因</span> <span>(</span><span>如系统掉电</span><span>)</span> <span>而中断，系统重启时，会根据日志记录来恢复中断前的写操作，而且这个过程费时极短</span><span>。</span><span>目前</span><span>Ext3</span><span>文件系统已经非常稳定可靠</span><span>。</span><span>它完全兼容</span><span>Ext2</span><span>文件系统</span><span>。</span><span>用户可以平滑地过渡到一个日志功能健全的文件系统中来</span><span>。</span><span>这实际上了也是</span><span>ext3</span><span>日志文件系统初始设计的初衷</span><span>。</span>

<span>Linux</span><span>文件系统在</span><span>windows</span><span>中是不能识别的，但是在</span><span>linux</span><span>系统中你可以挂载的</span><span>windows</span><span>的文件系统，</span><span>linux</span><span>目前支持</span><span>MS-DOS</span><span>，</span><span>VFAT</span><span>，</span><span>FAT</span><span>，</span><span>BSD</span><span>等格式</span><span>。</span><span>如果你使用的是</span><span>Redhat</span><span>或者</span><span>CentOS</span><span>，那么你不要妄图挂载</span><span>NFS</span><span>格式的文件到</span><span>linux</span><span>下，因为它不支持</span><span>NFS。</span><span>虽然有些版本的</span><span>linux</span><span>支持</span><span>NFS</span><span>，但不建议使用，因为目前的技术还不成熟</span><span>。</span>

<span>Ext3</span><span>文件系统为</span><span>Redhat/CentOS</span><span>默认使用的文件系统，除了</span><span>Ext3</span><span>文件系统外，有些</span><span>linux</span><span>发行版例如</span><span>SuSE</span><span>默认的文件系统为</span><span>reiserFS</span> <span>，</span><span>Ext3</span> <span>独特的优点就是易于转换，很容易在</span> <span>Ext2</span> <span>和</span> <span>Ext3</span> <span>之间相互转换，而具有良好的兼容性，其它优点</span> <span>ReiserFS</span> <span>都有，而且还比它做得更好</span><span>。</span><span>如高效的磁盘空间利用和独特的搜寻方式都是</span><span>Ext3</span> <span>所不具备的，速度上它也不能和</span> <span>ReiserFS</span><span>相媲美，在实际使用过程中，</span><span>reiserFS</span> <span>也更加安全高效，据说反删除功能也不错</span><span>。</span>

<span>ReiserFS</span> <span>的优势在于，它是基于</span> <span>B*Tree</span> <span>快速平衡树这种高效算法的文件系统，例如在处理小于</span> <span>1k</span> <span>的文件比</span> <span>Ext3</span> <span>快</span> <span>10</span> <span>倍</span><span>。</span><span>再一个就是</span> <span>ReiserFS</span> <span>空间浪费较少，它不会对一些小文件分配</span> <span>inode</span><span>，而是打包存放在同一个磁盘块</span> <span>(</span><span>簇</span><span>)</span> <span>中，</span><span>Ext2/Ext3</span> <span>是把它们单独存放在不同的簇上，如簇大小为</span> <span>4k</span><span>，那么</span> <span>2</span> <span>个</span> <span>100</span> <span>字节的文件会占用</span> <span>2</span> <span>个簇，</span><span>ReiserFS</span> <span>则只占用一个</span><span>。</span><span>当然</span> <span>ReiserFS</span> <span>也有缺点，就是每升级一个版本，都要将磁盘重新格式化一次</span><span>。</span>

## linux 文件类型 

<span>在前面的内容中简单介绍了普通文件</span><span>(-)</span><span>，目录</span><span>(d)</span><span>等，在</span><span>linux</span><span>文件系统中，主要有以下几种类型的文件</span><span>。</span>

<span>1</span><span>）正规文件（</span><span>regular file</span><span>）：就是一般类型的文件，当用</span><span>ls –l</span> <span>查看某个目录时，第一个属性为</span><span>”-“</span><span>的文件就是正规文件，或者叫普通文件</span><span>。</span><span>正规文件又可分成纯文字文件（</span><span>ascii</span><span>）和二进制文件（</span><span>binary</span><span>）</span><span>。</span><span>纯文本文件是可以通过</span><span>cat, more, less</span><span>等工具直接查看内容的，而二进制文件并不能</span><span>。</span><span>例如我们用的命令</span><span>/bin/ls</span> <span>这就是一个二进制文件</span><span>。</span>

<span>2</span><span>）目录（</span><span>directory</span><span>）：这个很容易理解，就是目录，跟</span><span>windows</span><span>下的文件夹一个意思，只不过在</span><span>linux</span><span>中我们不叫文件夹，而是叫做目录</span><span>。ls –l</span> <span>查看第一个属性为</span><span>”d”。</span>

<span>3</span><span>）连接档（</span><span>link</span><span>）：</span><span>ls –l</span> <span>查看第一个属性为</span> <span>“l”</span><span>，类似</span><span>windows</span><span>下的快捷方式</span><span>。</span><span>这种文件在</span><span>linux</span><span>中很常见，而且笔者在日常的系统运维工作中用的很多，所以你要特意留意一下这种类型的文件</span><span>。</span><span>在后续章节笔者会介绍</span><span>。</span>

<span>4</span><span>）设备档（</span><span>device</span><span>）：与系统周边相关的一些档案，通常都集中在</span> <span>/dev</span> <span>这个目录之下！通常又分为两种：区块</span> <span>(block)</span> <span>设备档</span><span>：就是一些储存数据，以提供系统存取的接口设备，简单的说就是硬盘啦！例如你的一号硬盘的代码是</span> <span>/dev/hda1</span> <span>等等的档案啦！第一个属性为</span> <span>“ b “</span><span>；字符</span> <span>(character)</span> <span>设备档</span><span>：亦即是一些串行端口的接口设备，例如键盘</span><span>、</span><span>鼠标等等！第一个属性为</span> <span>“ c “。</span>

<span>* linux</span> <span>文件后缀名</span>

<span>对于后缀名这个概念，相信你不陌生吧</span><span>。</span><span>在</span><span>linux</span><span>系统中，文件的后缀名并没有具体意义，也就是说，你加或者不加，都无所谓</span><span>。</span><span>但是为了容易区分，</span><span>linux</span><span>爱好者们都习惯给文件加一个后缀名，这样当用户看到这个文件名时就会很快想到它到底是一个什么文件</span><span>。</span><span>例如</span><span>1.sh, 2.tar.gz, my.cnf, test.zip</span><span>等等，如果你首次接触这些文件，你也许会感到很晕，没有关系，随着学习的深入，你就会逐渐的了解这些文件了</span><span>。</span><span>笔者所列举的几个文件名中</span><span>1.sh</span><span>代表它是一个</span><span>shell script</span> <span>，</span><span>2.tar.gz</span> <span>代表它是一个压缩包，</span><span>my.cnf</span> <span>代表它是一个配置文件，</span><span>test.zip</span> <span>代表它是一个压缩文件</span><span>。</span>

<span>另外需要你知道的是，早期</span><span>Unix</span><span>系统文件名最多允许</span><span>14</span><span>个字符，而新的</span><span>Unix</span><span>或者</span><span>linux</span><span>系统中，文件名最长可以到达</span> <span>256</span> <span>个字符！</span>

## linux 中的连接档 

<span>在讲连接档之前，需要你先理解</span><span>inode</span><span>的概念</span><span>。</span><span>什么是</span><span>inode</span><span>呢？这就需要你知道磁盘的整体构造</span><span>。</span><span>磁盘是有多个盘片（类似与光盘）重叠在一起构成的，而每个盘片上会有一个可以移动的磁头，这个磁头的作用就是用来读写数据的</span><span>。</span><span>磁头并不是一直在动，当磁头固定时，盘片转一圈，这一圈就是一个磁道了</span><span>。</span><span>很多个盘片同半径的那一圈的磁道总和称为磁柱</span><span>。</span><span>而由圆心向外画出直线，可以得到一个个扇区，如图二所示，一个扇区的物理量大约是</span> <span>512 bytes (</span> <span>约</span> <span>0.5K )。</span>

<span>![6_98.png.jpg](images/6_98.png.jpg)</span>

<span>图一</span>

<span>![6_99.png.jpg](images/6_99.png.jpg)</span>

<span>图二</span>

<span>知道了大体的硬盘构造之后，再来谈一谈怎么硬盘分割</span><span>( partition )</span><span>呢？我们在进行硬盘分割的时候，最小都是以磁柱为单位进行分割的，那么分割完成之后自然就是格式化</span><span>( format )</span><span>啰，在</span> <span>Linux</span> <span>里面我们在进行格式化的时候必须要考虑到</span> <span>Block</span> <span>与</span> <span>inode</span> <span>的信息，这个</span> <span>block</span> <span>还好理解，他是我们磁盘可以记录的最小单位，是由数个</span> <span>sector</span> <span>所组成的，所以他的大小通常为</span> <span>n*512 bytes</span> <span>，例如</span> <span>4K 。</span><span>那么</span> <span>inode</span> <span>是什么？</span> <span>Block</span> <span>是记录</span><span>“</span><span>档案内容数据</span><span>”</span><span>的地区，而</span> <span>inode</span> <span>则是记录</span><span>“</span><span>该档案的属性</span><span>、</span><span>及该档案放置在哪一个</span> <span>Block</span> <span>之内</span><span>”</span><span>的信息！所以，每个档案都会占用到至少一个</span> <span>inode 。</span><span>而当我们</span> <span>Linux</span> <span>系统要找到这个档案时，他会先去搜寻</span> <span>inode table</span> <span>找到这个档案的属性及数据放置的地区，然后再到数据去找到数据存放的</span> <span>Block</span> <span>进而将数据取出利用</span><span>。</span><span>这个</span> <span>inode</span> <span>数目在一开始就会被设定好，他的设定方式通常是利用</span> <span>(</span> <span>硬盘大小</span> <span>/</span> <span>一个容量</span> <span>)</span><span>，这个容量至少应该比</span> <span>Block</span> <span>要大一些较佳，例如刚刚的</span> <span>Block</span> <span>订为</span> <span>4K</span> <span>，那么</span> <span>inode</span> <span>可以订为</span> <span>8K</span> <span>左右</span><span>。</span><span>所以，一颗</span> <span>1GB</span> <span>的硬盘，如果以</span> <span>8K</span> <span>来规划他的</span> <span>inode</span> <span>数时，他的</span> <span>inode</span> <span>就会有</span> <span>131072</span> <span>个</span> <span>inode</span> <span>啦！而一个</span> <span>inode</span> <span>的大小为</span> <span>128 bytes</span> <span>这么大！这么一来的话，我们就可以清楚的知道了，那就是一个</span> <span>partition</span> <span>格式化为一个</span> <span>filesystem</span> <span>之后，基本上，他一定会有</span> <span>inode table</span> <span>与</span> <span>data area</span> <span>两个区块，一个用来记录档案的信息与该档案放置的</span> <span>block</span> <span>区块，一个用来记录档案的内容！</span>

<span>由于我们</span> <span>Linux</span> <span>在读取数据的时候，是先查询</span> <span>inode table</span> <span>以得到数据是放在那个</span> <span>Block</span> <span>里面，然后再去该</span> <span>Block</span> <span>里面读取真正的数据内容！然后，那个</span> <span>block</span> <span>是我们在格式化硬盘的时候规定出来的一个值，这个</span> <span>block</span> <span>是由</span> <span>2</span> <span>的</span> <span>n</span> <span>次方个</span><span>sector</span> <span>所集结而成的！所以，他是</span> <span>0.5K</span> <span>的倍数！假设我们</span> <span>block</span> <span>规划为</span> <span>4KBytes</span> <span>好了，那么由于一个</span> <span>inode</span> <span>与一个</span><span>block</span> <span>最多均只纪录一个档案，所以，如果你的一个档案有</span> <span>0.1 K bytes</span> <span>这么大时，你要晓得的是，由于你的</span> <span>block</span> <span>为</span> <span>4K bytes</span> <span>，因此，你就会有</span> <span>3.9 Kbytes</span> <span>的空间浪费掉！所以，当你在格式化硬盘的时候，请千万注意到你的系统未来的使用方向</span><span>。</span>

## ln 建立连接档

<span>前面提到过两次连接档的概念，现在终于该好好介绍下这部分内容了</span><span>。</span><span>连接档分为两种，硬连接（</span><span>hard link</span><span>）和软连接（</span><span>symbolic link</span><span>）</span><span>。</span>

<span>**Hard Links**</span><span>**：**</span><span>上面内容中说过，当系统要读取一个文件时，就会先去读</span><span>inode table</span><span>，然后再去根据</span><span>inode</span><span>中的信息到块区域去将数据取出来</span><span>。</span><span>而</span><span>hard link</span> <span>是直接再建立一个</span><span>inode</span><span>连接到文件放置的块区域</span><span>。</span><span>也就是说，进行</span><span>hard link</span><span>的时候实际上该文件内容没有任何变化，只是增加了一个指到这个文件的</span><span>inode</span><span>，不过这样一来就会有个问题，因为增加的</span><span>inode</span><span>会连接到块区域，而目录本身仅仅消耗</span><span>inode</span><span>而已，那么</span><span>hard link</span><span>就不能连接目录了</span><span>。</span><span>请你记住，</span><span>hard link</span> <span>有两个限制：</span><span>1</span> <span>不能跨文件系统，因为不通的文件系统有不同的</span><span>inode table</span><span>；</span> <span>2</span> <span>不能连接目录</span><span>。</span>

<span>**Symbolic Links**</span><span>**：**</span><span>跟</span><span>hard link</span><span>不同，这个是建立一个独立的文件，而这个文件的作用是当读取这个连接文件时，它会把读取的行为转发到该文件所</span><span>link</span><span>的文件上</span><span>。</span><span>这样讲，也许比较绕口，那么就来举一个例子</span><span>。</span><span>现在有文件</span><span>a</span><span>，我们做了一个软连接文件</span><span>b</span><span>（只是一个连接文件，非常小），</span><span>b</span><span>指向了文件</span><span>a。</span><span>当读取</span><span>b</span><span>时，那么</span><span>b</span><span>就会把读取的动作转发到</span><span>a</span><span>上，这样就读取到了文件</span><span>a。</span><span>所以，当你删除文件</span><span>a</span><span>时，文件</span><span>b</span><span>并不会被删除，但是再读取</span><span>b</span><span>时，会提示无法打开文件</span><span>。</span><span>而，当你删除</span><span>b</span><span>时，</span><span>a</span><span>是不会有任何影响的</span><span>。</span>

<span>看样子，似乎</span> <span>hard link</span> <span>比较安全，因为即使某一个</span> <span>inode</span> <span>被杀掉了，只要有任何一个</span> <span>inode</span> <span>存在，那么该文件就不会不见！不过，不幸的是，由于</span> <span>Hard Link</span> <span>的限制太多了，包括无法做目录的</span> <span>link</span> <span>，所以在用途上面是比较受限的！反而是</span> <span>Symbolic Link</span> <span>的使用方向较广！那么如何建立软连接和硬连接呢？这就用到了</span><span>ln</span> <span>命令</span><span>。</span>

<span>ln</span> <span>语法：</span> <span>ln [-s] [</span><span>来源文件</span><span>] [</span><span>目的文件</span><span>]</span>

<span>ln</span> <span>常用的选项就一个</span><span>-s</span> <span>，如果不加就是建立硬连接，加上就建立软连接</span><span>。</span>

<span>![6_100.png.jpg](images/6_100.png.jpg)</span>

<span>在建立硬连接前后，</span><span>123</span><span>目录所占空间大小并没有改变</span><span>。</span>

<span>![6_101.png.jpg](images/6_101.png.jpg)</span>

<span>当把源文件删除后，空间仍旧没有变化</span><span>。</span><span>说明了删除一个文件其实只是删除了</span><span>inode</span><span>信息</span><span>。</span>

<span>![6_102.png.jpg](images/6_102.png.jpg)</span>

<span>不能创建目录的硬连接</span><span>。</span>

<span>![6_103.png.jpg](images/6_103.png.jpg)</span>

<span>建立软连接后，</span><span>456</span><span>目录增加了</span><span>4k</span>

<span>![6_104.png.jpg](images/6_104.png.jpg)</span>

<span>删除源文件后会提示</span><span>“</span><span>没有这个文件</span><span>”</span><span>的错误</span><span>。</span>

<span>![6_105.png.jpg](images/6_105.png.jpg)</span>

<span>目录是可以软连接的</span><span>。</span>

<span>![6_106.png.jpg](images/6_106.png.jpg)</span>

<span>删除软连接对源文件没有任何影响</span><span>。</span>

