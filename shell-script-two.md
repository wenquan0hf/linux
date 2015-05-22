# shell 脚本 

<span>终于到</span><span>shell</span> <span>脚本这章了，在以前笔者卖了好多关子说</span><span>shell</span><span>脚本怎么怎么重要，确实</span><span>shell</span><span>脚本在</span><span>linux</span><span>系统管理员的运维工作中非常非常重要</span><span>。</span><span>下面笔者就带你正式进入</span><span>shell</span><span>脚本的世界吧</span><span>。</span>

<span>到现在为止，你明白什么是</span><span>shell</span><span>脚本吗？如果明白最好了，不明白也没有关系，相信随着学习的深入你就会越来越了解到底什么是</span><span>shell</span><span>脚本</span><span>。</span><span>首先它是一个脚本，并不能作为正式的编程语言</span><span>。</span><span>因为是跑在</span><span>linux</span><span>的</span><span>shell</span><span>中，所以叫</span><span>shell</span><span>脚本</span><span>。</span><span>说白了，</span><span>shell</span><span>脚本就是一些命令的集合</span><span>。</span><span>举个例子，我想实现这样的操作：</span><span>1</span><span>）进入到</span><span>/tmp/</span><span>目录；</span><span>2</span><span>）列出当前目录中所有的文件名；</span><span>3</span><span>）把所有当前的文件拷贝到</span><span>/root/</span><span>目录下；</span><span>4</span><span>）删除当前目录下所有的文件</span><span>。</span><span>简单的</span><span>4</span><span>步在</span><span>shell</span><span>窗口中需要你敲</span><span>4</span><span>次命令，按</span><span>4</span><span>次回车</span><span>。</span><span>这样是不是很麻烦？当然这</span><span>4</span><span>步操作非常简单，如果是更加复杂的命令设置需要几十次操作呢？那样的话一次一次敲键盘会很麻烦</span><span>。</span><span>所以不妨把所有的操作都记录到一个文档中，然后去调用文档中的命令，这样一步操作就可以完成</span><span>。</span><span>其实这个文档呢就是</span><span>shell</span><span>脚本了，只是这个</span><span>shell</span><span>脚本有它特殊的格式</span><span>。</span>

<span>Shell</span><span>脚本能帮助我们很方便的去管理服务器，因为我们可以指定一个任务计划定时去执行某一个</span><span>shell</span><span>脚本实现我们想要需求</span><span>。</span><span>这对于</span><span>linux</span><span>系统管理员来说是一件非常值得自豪的事情</span><span>。</span><span>现在的</span><span>139</span><span>邮箱很好用，发邮件的同时还可以发一条邮件通知的短信给用户，利用这点，我们就可以在我们的</span><span>linux</span><span>服务器上部署监控的</span><span>shell</span><span>脚本，比如网卡流量有异常了或者服务器</span><span>web</span><span>服务器停止了就可以发一封邮件给管理员，同时发送给管理员一个报警短信这样可以让我们及时的知道服务器出问题了</span><span>。</span>

<span>有一个问题需要约定一下，</span><span>凡是自定义的脚本建议放到</span><span>/usr/local/sbin/</span><span>目录下</span><span>，这样做的目的是，一来可以更好的管理文档；二来以后接管你的管理员都知道自定义脚本放在哪里，方便维护</span><span>。</span>

<span>【</span><span>**shell**</span><span>**脚本的基本结构以及如何执行**</span><span>】</span>

<span>![14_1.png.jpg](images/14_1.png.jpg)</span>

<span>Shell</span><span>脚本通常都是以</span><span>.sh</span> <span>为后缀名的，这个并不是说不带</span><span>.sh</span><span>这个脚本就不能执行，只是大家的一个习惯而已</span><span>。</span><span>所以，以后你发现了</span><span>.sh</span><span>为后缀的文件那么它一定会是一个</span><span>shell</span><span>脚本了</span><span>。test.sh</span><span>中第一行一定是</span> <span>“#! /bin/bash”</span> <span>它代表的意思是，该文件使用的是</span><span>bash</span><span>语法</span><span>。</span><span>如果不设置该行，那么你的</span><span>shell</span><span>脚本就不能被执行</span><span>。’#’</span><span>表示注释，在前面讲过的</span><span>。</span><span>后面跟一些该脚本的相关注释内容以及作者和创建日期或者版本等等</span><span>。</span><span>当然这些注释并非必须的，如果你懒的很，可以省略掉，但是笔者不建议省略</span><span>。</span><span>因为随着你工作时间的增加，你写的</span><span>shell</span><span>脚本也会越来越多，如果有一天你回头查看你写的某个脚本时，很有可能忘记该脚本是用来干什么的以及什么时候写的</span><span>。</span><span>所以写上注释是有必要的</span><span>。</span><span>另外系统管理员并非你一个，如果是其他管理员查看你的脚本，他看不懂岂不是很郁闷</span><span>。</span><span>该脚本再往下面则为要运行的命令了</span><span>。</span>

<span>![14_7.png.jpg](images/14_7.png.jpg)</span>

<span>Shell</span><span>脚本的执行很简单，直接</span><span>”sh filename “</span> <span>即可，另外你还可以这样执行</span>

<span>![14_8.png.jpg](images/14_8.png.jpg)</span>

<span>默认我们用</span><span>vim</span><span>编辑的文档是不带有执行权限的，所以需要加一个执行权限，那样就可以直接使用</span><span>’./filename’</span> <span>执行这个脚本了</span><span>。</span><span>另外使用</span><span>sh</span><span>命令去执行一个</span><span>shell</span><span>脚本的时候是可以加</span><span>-x</span><span>选项来查看这个脚本执行过程的，这样有利于我们调试这个脚本哪里出了问题</span><span>。</span>

<span>![14_9.png.jpg](images/14_9.png.jpg)</span>

<span>该</span><span>shell</span><span>脚本中用到了</span><span>’date’</span><span>这个命令，它的作用就是用来打印当前系统的时间</span><span>。</span><span>其实在</span><span>shell</span><span>脚本中</span><span>date</span><span>使用率非常高</span><span>。</span><span>有几个选项笔者常常在</span><span>shell</span><span>脚本中用到：</span>

<span>![14_10.png.jpg](images/14_10.png.jpg)</span>

<span>%Y</span><span>表示年，</span><span>%m</span><span>表示月，</span><span>%d</span><span>表示日期，</span><span>%H</span><span>表示小时，</span><span>%M</span><span>表示分钟，</span><span>%S</span><span>表示秒</span>

<span>![14_11.png.jpg](images/14_11.png.jpg)</span>

<span>注意</span><span>%y</span><span>和</span><span>%Y</span><span>的区别</span><span>。</span>

<span>![14_21.png.jpg](images/14_21.png.jpg)</span>

<span>-d</span> <span>选项也是经常要用到的，它可以打印</span><span>n</span><span>天前或者</span><span>n</span><span>天后的日期，当然也可以打印</span><span>n</span><span>个月</span><span>/</span><span>年前或者后的日期</span><span>。</span>

![14_22.png.jpg](images/14_22.png.jpg)

<span>另外星期几也是常用的</span>

<span>![14_23.png.jpg](images/14_23.png.jpg)</span>

<span>**【shell**</span><span>**脚本中的变量**</span><span>**】**</span>

<span>在</span><span>shell</span><span>脚本中使用变量显得我们的脚本更加专业更像是一门语言，开个玩笑，变量的作用当然不是为了专业</span><span>。</span><span>如果你写了一个长达</span><span>1000</span><span>行的</span><span>shell</span><span>脚本，并且脚本中出现了某一个命令或者路径几百次</span><span>。</span><span>突然你觉得路径不对想换一下，那岂不是要更改几百次？你固然可以使用批量替换的命令，但是也是很麻烦，并且脚本显得臃肿了很多</span><span>。</span><span>变量的作用就是用来解决这个问题的</span><span>。</span>

<span>![14_24.png.jpg](images/14_24.png.jpg)</span>

<span>在</span><span>test2.sh</span><span>中使用到了反引号，你是否还记得它的作用？</span><span>’d’</span><span>和</span><span>’d1’</span><span>在脚本中作为变量出现，定义变量的格式为</span> <span>“</span><span>变量名</span><span>=</span><span>变量的值</span><span>”。</span><span>当在脚本中引用变量时需要加上</span><span>’$’</span><span>符号，这跟前面讲的在</span><span>shell</span><span>中自定义变量是一致的</span><span>。</span><span>下面看看脚本执行结果吧</span><span>。</span>

<span>![14_25.png.jpg](images/14_25.png.jpg)</span>

<span>下面我们用</span><span>shell</span><span>计算两个数的和</span><span>。</span>

<span>![14_26.png.jpg](images/14_26.png.jpg)</span>

<span>数学计算要用</span><span>’[ ]’</span><span>括起来并且外头要带一个</span><span>’$’。</span><span>脚本结果为：</span>

<span>![14_27.png.jpg](images/14_27.png.jpg)</span>

<span>Shell</span><span>脚本还可以和用户交互</span><span>。</span>

<span>![14_28.png.jpg](images/14_28.png.jpg)</span>

<span>这就用到了</span><span>read</span><span>命令了，它可以从标准输入获得变量的值，后跟变量名</span><span>。”read x”</span><span>表示</span><span>x</span><span>变量的值需要用户通过键盘输入得到</span><span>。</span><span>脚本执行过程如下：</span>

<span>![14_29.png.jpg](images/14_29.png.jpg)</span>

<span>我们不妨加上</span><span>-x</span><span>选项再来看看这个执行过程：</span>

<span>![14_44.png.jpg](images/14_44.png.jpg)</span>

<span>在</span><span>test4.sh</span><span>中还有更加简洁的方式</span><span>。</span>

<span>![14_45.png.jpg](images/14_45.png.jpg)</span>

read -p <span>选项类似</span><span>echo</span><span>的作用</span><span>。</span><span>执行如下：</span>

<span>![14_46.png.jpg](images/14_46.png.jpg)</span>

<span>你有没有用过这样的命令</span><span>”/etc/init.d/iptables restart “</span> <span>前面的</span><span>/etc/init.d/iptables</span> <span>文件其实就是一个</span><span>shell</span><span>脚本，为什么后面可以跟一个</span><span>”restart”?</span> <span>这里就涉及到了</span><span>shell</span><span>脚本的预设变量</span><span>。</span><span>实际上，</span><span>shell</span><span>脚本在执行的时候后边是可以跟变量的，而且还可以跟多个</span><span>。</span><span>不妨笔者写一个脚本，你就会明白了</span><span>。</span>

<span>![14_47.png.jpg](images/14_47.png.jpg)</span>

<span>执行过程如下：</span>

<span>![14_48.png.jpg](images/14_48.png.jpg)</span>

<span>在脚本中，你会不会奇怪，哪里来的</span><span>$1</span><span>和</span><span>$2</span><span>，这其实就是</span><span>shell</span><span>脚本的预设变量，其中</span><span>$1</span><span>的值就是在执行的时候输入的</span><span>1</span><span>，而</span><span>$2</span><span>的值就是执行的时候输入的</span><span>$2</span><span>，当然一个</span><span>shell</span><span>脚本的预设变量是没有限制的，这回你明白了吧</span><span>。</span><span>另外还有一个</span><span>$0</span><span>，不过它代表的是脚本本身的名字</span><span>。</span><span>不妨把脚本修改一下</span><span>。</span>

<span>![14_49.png.jpg](images/14_49.png.jpg)</span>

<span>执行结果想必你也猜到了吧</span><span>。</span>

<span>![14_50.png.jpg](images/14_50.png.jpg)</span>

<span>**【shell**</span><span>**脚本中的逻辑判断**</span><span>**】**</span>

<span>如果你学过</span><span>C</span><span>或者其他语言，相信你不会对</span><span>if</span> <span>陌生，在</span><span>shell</span><span>脚本中我们同样可以使用</span><span>if</span><span>逻辑判断</span><span>。</span><span>在</span><span>shell</span><span>中</span><span>if</span><span>判断的基本语法为：</span>

<span>**1**</span><span>**）不带**</span><span>**else**</span>

<span>if</span> <span>判断语句</span><span>; then</span>

<span>command</span>

<span>fi</span>

<span>![14_51.png.jpg](images/14_51.png.jpg)</span>

<span>在</span><span>if1.sh</span><span>中出现了</span> <span>((a<60))</span><span>这样的形式，这是</span><span>shell</span><span>脚本中特有的格式，用一个小括号或者不用都会报错，请记住这个格式，即可</span><span>。</span><span>执行结果为：</span>

<span>![14_52.png.jpg](images/14_52.png.jpg)</span>

<span>**2**</span><span>**）带有**</span><span>**else**</span>

<span>if</span> <span>判断语句</span> <span>; then</span>

<span>command</span>

<span>else</span>

<span>command</span>

<span>fi</span>

<span>![14_53.png.jpg](images/14_53.png.jpg)</span>

<span>执行结果为：</span>

<span>![14_54.png.jpg](images/14_54.png.jpg)</span>

<span>**3**</span><span>**）带有**</span><span>**elif**</span>

<span>if</span> <span>判断语句一</span> <span>; then</span>

<span>command</span>

<span>elif</span> <span>判断语句二</span><span>; then</span>

<span>command</span>

<span>else</span>

<span>command</span>

<span>fi</span>

<span>![14_55.png.jpg](images/14_55.png.jpg)</span>

<span>这里的</span> <span>&&</span> <span>表示</span><span>“</span><span>并且</span><span>”</span><span>的意思，当然你也可以使用</span> <span>||</span> <span>表示</span><span>“</span><span>或者</span><span>”</span><span>，执行结果：</span>

<span>![14_56.png.jpg](images/14_56.png.jpg)</span>

<span>以上只是简单的介绍了</span><span>if</span><span>语句的结构</span><span>。</span><span>在判断数值大小除了可以用</span><span>”(( ))”</span><span>的形式外，还可以使用</span><span>”[ ]”。</span><span>但是就不能使用</span><span>>, < , =</span> <span>这样的符号了，要使用</span> <span>-lt</span> <span>（小于），</span><span>-gt</span> <span>（大于），</span><span>-le</span> <span>（小于等于），</span><span>-ge</span> <span>（大于等于），</span><span>-eq</span> <span>（等于），</span><span>-ne</span> <span>（不等于）</span><span>。</span>

<span>![14_57.png.jpg](images/14_57.png.jpg)</span>

<span>再看看</span><span>if</span><span>中使用</span> <span>&&</span> <span>和</span> <span>||</span><span>的情况</span><span>。</span>

<span>![14_71.png.jpg](images/14_71.png.jpg)</span>

<span>shell</span> <span>脚本中</span><span>if</span><span>还经常判断关于档案属性，比如判断是普通文件还是目录，判断文件是否有读写执行权限等</span><span>。</span><span>常用的也就几个选项：</span>

<span>-e</span> <span>：判断文件或目录是否存在</span>

<span>-d</span> <span>：判断是不是目录，并是否存在</span>

<span>-f</span> <span>：判断是否是普通文件，并存在</span>

<span>-r</span> <span>：判断文档是否有读权限</span>

<span>-w</span> <span>：判断是否有写权限</span>

<span>-x</span> <span>：判断是否可执行</span>

<span>使用</span><span>if</span><span>判断时，具体格式为：</span> <span>if [ -e filename ] ; then</span>

<span>![14_72.png.jpg](images/14_72.png.jpg)</span>

<span>在</span><span>shell</span> <span>脚本中，除了用</span><span>if</span><span>来判断逻辑外，还有一种常用的方式，那就是</span><span>case</span><span>了</span><span>。</span><span>具体格式为：</span>

<span>case</span> <span>变量</span> <span>in</span>

<span>value1)</span>

<span>command</span>

<span>;;</span>

<span>value2)</span>

<span>command</span>

<span>;;</span>

<span>value3)</span>

<span>command</span>

<span>;;</span>

<span>*)</span>

<span>command</span>

<span>;;</span>

<span>esac</span>

<span>上面的结构中，不限制</span><span>value</span><span>的个数，</span><span>*</span><span>则代表除了上面的</span><span>value</span><span>外的其他值</span><span>。</span><span>下面笔者写一个判断输入数值是奇数或者偶数的脚本</span><span>。</span>

<span>![14_73.png.jpg](images/14_73.png.jpg)</span>

<span>$a</span> <span>的值或为</span><span>1</span><span>或为</span><span>0</span><span>，执行结果为：</span>

<span>![14_74.png.jpg](images/14_74.png.jpg)</span>

<span>也可以看一下执行过程：</span>

<span>![14_75.png.jpg](images/14_75.png.jpg)</span>

<span>case</span><span>脚本常用于编写系统服务的启动脚本，例如</span><span>/etc/init.d/iptables</span><span>中就用到了，你不妨去查看一下</span><span>。</span>

<span>**【shell**</span><span>**脚本中的循环**</span><span>**】**</span>

<span>Shell</span><span>脚本中也算是一门简易的编程语言了，当然循环是不能缺少的</span><span>。</span><span>常用到的循环有</span><span>for</span><span>循环和</span><span>while</span><span>循环</span><span>。</span><span>下面就分别介绍一下两种循环的结构</span><span>。</span>

<span>![14_76.png.jpg](images/14_76.png.jpg)</span>

<span>脚本中的</span><span>seq 1 5</span> <span>表示从</span><span>1</span><span>到</span><span>5</span><span>的一个序列</span><span>。</span><span>你可以直接运行这个命令试下</span><span>。</span><span>脚本执行结果为：</span>

<span>![14_77.png.jpg](images/14_77.png.jpg)</span>

<span>通过这个脚本就可以看到</span><span>for</span><span>循环的基本结构</span><span>：</span>

<span>for</span> <span>变量名</span> <span>in</span> <span>循环的条件；</span> <span>do</span>

<span>command</span>

<span>done</span>

<span>![14_78.png.jpg](images/14_78.png.jpg)</span>

<span>循环的条件那一部分也可以写成这样的形式，中间用空格隔开即可</span><span>。</span><span>你也可以试试，</span><span>for i in `ls`; do echo $i; done</span> <span>和</span> <span>for i in `cat test.txt`</span><span>；</span> <span>do echo $i; done</span>

<span>![14_79.png.jpg](images/14_79.png.jpg)</span>

<span>再来看看这个</span><span>while</span><span>循环，基本格式为：</span>

<span>while</span> <span>条件</span><span>; do</span>

<span>command</span>

<span>done</span>

<span>脚本的执行结果为：</span>

<span>![14_80.png.jpg](images/14_80.png.jpg)</span>

<span>另外你可以把循环条件忽略掉，笔者常常这样写监控脚本</span><span>。</span>

<span>while :; do</span>

<span>command</span>

<span>done</span>

<span>**【shell**</span><span>**脚本中的函数**</span><span>**】**</span>

<span>如果你学过开发，肯定知道函数的作用</span><span>。</span><span>如果你是刚刚接触到这个概念的话，也没有关系，其实很好理解的</span><span>。</span><span>函数就是把一段代码整理到了一个小单元中，并给这个小单元起一个名字，当用到这段代码时直接调用这个小单元的名字即可</span><span>。</span><span>有时候脚本中的某段代总是重复使用，如果写成函数，每次用到时直接用函数名代替即可，这样就节省了时间还节省了空间</span><span>。</span>

<span>![14_81.png.jpg](images/14_81.png.jpg)</span>

<span>fun.sh</span> <span>中的</span><span>sum()</span> <span>为自定义的函数，在</span><span>shell</span><span>脚本中要用</span>

<span>function</span> <span>函数名</span><span>() {</span>

<span>command</span>

<span>}</span>

<span>这样的格式去定义函数</span><span>。</span>

<span>上个脚本执行过程如下：</span>

<span>![14_82.png.jpg](images/14_82.png.jpg)</span>

<span>有一点笔者要提醒你一下，在</span><span>shell</span><span>脚本中，函数一定要写在最前面，不能出现在中间或者最后，因为函数是要被调用的，如果还没有出现就被调用，肯定是会出错的</span><span>。</span>

<span>Shell</span><span>脚本大体上就介绍这么多了，笔者所举的例子都是最基础的，所以即使你把所有例子完全掌握也不代表你的</span><span>shell</span><span>脚本编写能力有多么好</span><span>。</span><span>所以剩下的日子里你尽量要多练习，多写脚本，你写的脚本越多，你的能力就越强</span><span>。</span><span>希望你能够找专门介绍</span><span>shell</span><span>脚本的书籍深入的去研究一下它</span><span>。</span><span>随后笔者将给你留几个</span><span>shell</span><span>脚本的练习题，你最好不要偷懒</span><span>。</span>

<span>1\.</span> <span>编写</span><span>shell</span><span>脚本，计算</span><span>1-100</span><span>的和；</span>

<span>2\.</span> <span>编写</span><span>shell</span><span>脚本，要求输入一个数字，然后计算出从</span><span>1</span><span>到输入数字的和，要求，如果输入的数字小于</span><span>1</span><span>，则重新输入，直到输入正确的数字为止；</span>

<span>3\.</span> <span>编写</span><span>shell</span><span>脚本，把</span><span>/root/</span><span>目录下的所有目录（只需要一级）拷贝到</span><span>/tmp/</span><span>目录下；</span>

<span>4\.</span> <span>编写</span><span>shell</span><span>脚本，批量建立用户</span><span>user_00, user_01, … ,user_100</span><span>并且所有用户同属于</span><span>users</span><span>组；</span>

<span>5\.</span> <span>编写</span><span>shell</span><span>脚本，截取文件</span><span>test.log</span><span>中包含关键词</span><span>’abc’</span><span>的行中的第一列（假设分隔符为</span><span>”:”</span><span>），然后把截取的数字排序（假设第一列为数字），然后打印出重复次数超过</span><span>10</span><span>次的列；</span>

<span>6\.</span> <span>编写</span><span>shell</span><span>脚本，判断输入的</span><span>IP</span><span>是否正确（</span><span>IP</span><span>的规则是，</span><span>n1.n2.n3.n4</span><span>，其中</span><span>1<n1<255, 0<n2<255, 0<n3<255, 0<n4<255</span><span>）</span><span>。</span>

<span>以下为练习题答案：</span>

<span>1\. #! /bin/bash</span>

<span>sum=0</span>

<span>for i in `seq 1 100`; do</span>

<span>sum=$[$i+$sum]</span>

<span>done</span>

<span>echo $sum</span>

<span>2\. #! /bin/bash</span>

<span>n=0</span>

<span>while [ $n -lt "1" ]; do</span>

<span>read -p "Please input a number, it must greater than "1":" n</span>

<span>done</span>

<span> </span>

<span>sum=0</span>

<span>for i in `seq 1 $n`; do</span>

<span>sum=$[$i+$sum]</span>

<span>done</span>

<span>echo $sum</span>

<span> </span>

<span>3\. #! /bin/bash</span>

<span>for f in `ls /root/`; do</span>

<span>if [ -d $f ] ; then</span>

<span>cp -r $f /tmp/</span>

<span>fi</span>

<span>done</span>

<span> </span>

<span>4\. #! /bin/bash</span>

<span>groupadd users</span>

<span>for i in `seq 0 9`; do</span>

<span>useradd -g users user_0$i</span>

<span>done</span>

<span> </span>

<span>for j in `seq 10 100`; do</span>

<span>useradd -g users user_$j</span>

<span>done</span>

<span> </span>

<span>5\. #! /bin/bash</span>

<span>awk -F':' '$0~/abc/ ' test.log >/tmp/n.txt</span>

<span>sort -n n.txt |uniq -c |sort -n >/tmp/n2.txt</span>

<span>awk '$1>10 ' /tmp/n2.txt</span>

<span> </span>

<span>6\. #! /bin/bash</span>

<span>checkip() {</span>

<span>if echo $1 |egrep -q '^[0-9]\.[0-9]\.[0-9]\.[0-9]/span> ; then</span>

<span>a=`echo $1 | awk -F. ''`</span>

<span>b=`echo $1 | awk -F. ''`</span>

<span>c=`echo $1 | awk -F. ''`</span>

<span>d=`echo $1 | awk -F. ''`</span>

<span> </span>

<span>for n in $a $b $c $d; do</span>

<span>if [ $n -ge 255 ] || [ $n -le 0 ]; then</span>

<span>echo "the number of the IP should less than 255 and greate than 0"</span>

<span>return 2</span>

<span>fi</span>

<span>done</span>

<span>else</span>

<span>echo "The IP you input is something wrong, the format is like 192.168.100.1"</span>

<span>return 1</span>

<span>fi</span>

<span>}</span>

<span> </span>

<span>rs=1</span>

<span>while [ $rs -gt 0 ]; do</span>

<span>read -p "Please input the ip:" ip</span>

<span>checkip $ip</span>

<span>rs=`echo $?`</span>

<span>done</span>

<span>echo "The IP is right!"</span>

