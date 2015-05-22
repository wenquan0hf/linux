# 正则表达式

<span>这部分内容可以说是学习</span><span>shell</span><span>脚本之前必学的内容</span><span>。</span><span>如果你这部分内容学的越好，那么你的</span><span>shell</span><span>脚本编写能力就会越强</span><span>。</span><span>所以不要嫌这部分内容啰嗦，也不要怕麻烦，要用心学习</span><span>。</span><span>一定要多加练习，练习多了就能熟练掌握了</span><span>。</span>

<span>在计算机科学中，正则表达式是这样解释的：它是指一个用来描述或者匹配一系列符合某个句法规则的字符串的单个字符串</span><span>。</span><span>在很多文本编辑器或其他工具里，正则表达式通常被用来检索和</span><span>/</span><span>或替换那些符合某个模式的文本内容</span><span>。</span><span>许多程序设计语言都支持利用正则表达式进行字符串操作</span><span>。</span><span>对于系统管理员来讲，正则表达式贯穿在我们的日常运维工作中，无论是查找某个文档，抑或查询某个日志文件分析其内容，都会用到正则表达式</span><span>。</span>

<span>其实正则表达式，只是一种思想，一种表示方法</span><span>。</span><span>只要我们使用的工具支持表示这种思想那么这个工具就可以处理正则表达式的字符串</span><span>。</span><span>常用的工具有</span><span>grep, sed, awk</span> <span>等，下面笔者就介绍一下这三种工具的使用方法</span><span>。</span>

<span>【</span><span>**grep / egrep**</span><span>】</span>

<span>笔者在前面的内容中多次提到并用到</span><span>grep</span><span>命令，可见它的重要性</span><span>。</span><span>所以好好学习一下这个重要的命令吧</span><span>。</span><span>你要知道的是</span><span>grep</span><span>连同下面讲的</span><span>sed, awk</span><span>都是针对文本的行才操作的</span><span>。</span>

<span>语法：</span> <span>grep [-cinvABC] ‘word’ filename</span>

<span>-c</span> <span>：打印符合要求的行数</span>

<span>-i</span> <span>：忽略大小写</span>

<span>-n</span> <span>：在输出符合要求的行的同时连同行号一起输出</span>

<span>-v</span> <span>：打印不符合要求的行</span>

<span>-A</span> <span>：后跟一个数字（有无空格都可以），例如</span> <span>–A2</span><span>则表示打印符合要求的行以及下面两行</span>

<span>-B</span> <span>：后跟一个数字，例如</span> <span>–B2</span> <span>则表示打印符合要求的行以及上面两行</span>

<span>-C</span> <span>：后跟一个数字，例如</span> <span>–C2</span> <span>则表示打印符合要求的行以及上下各两行</span>

<span>![13_1.png.jpg](images/13_1.png.jpg)</span>

<span>以下，笔者举几个小例子帮助你好好掌握这个</span><span>grep</span><span>工具的用法</span><span>。</span>

<span>**a.** </span><span>**过滤出带有某个关键词的行并输出行号**</span>

<span>![13_7.png.jpg](images/13_7.png.jpg)</span>

<span>**b.** </span><span>**过滤不带有某个关键词的行，并输出行号**</span>

<span>![13_8.png.jpg](images/13_8.png.jpg)</span>

<span>**c.** </span><span>**过滤出所有包含数字的行**</span>

<span>![13_9.png.jpg](images/13_9.png.jpg)</span>

<span>在前面也提到过这个</span><span>”[ ]”</span><span>的应用，如果是数字的话就用</span><span>[0-9]</span><span>这样的形式，当然有时候也可以用这样的形式</span><span>[15]</span><span>即只含有</span><span>1</span><span>或者</span><span>5</span><span>，注意，它不会认为是</span><span>15。</span><span>如果要过滤出数字以及大小写字母则要这样写</span><span>[0-9a-zA-Z]。</span><span>另外</span><span>[ ]</span><span>还有一种形式，就是</span><span>[^</span><span>字符</span><span>]</span> <span>表示除</span><span>[ ]</span><span>内的字符之外的字符</span><span>。</span>

<span>![13_10.png.jpg](images/13_10.png.jpg)</span>

<span>这就表示筛选包含</span><span>oo</span><span>字符串，但是不包含</span><span>r</span><span>字符</span><span>。</span>

<span>**d.** </span><span>**过滤出文档中以某个字符开头或者以某个字符结尾的行**</span>

<span>![13_11.png.jpg](images/13_11.png.jpg)</span>

<span>在正则表达式中，</span><span>”^”</span><span>表示行的开始，</span><span>”$”</span><span>表示行的结尾，那么空行则表示</span><span>”^$”,</span><span>如果你只想筛选出非空行，则可以使用</span> <span>“grep -v ‘^$’ filename”</span><span>得到你想要的结果</span><span>。</span><span>现在想一下，如何打印出不以英文字母开头的行呢？</span>

<span>![13_21.png.jpg](images/13_21.png.jpg)</span>

<span>**e.** </span><span>**过滤任意一个字符与重复字符**</span>

<span>![13_22.png.jpg](images/13_22.png.jpg)</span>

<span>“.”</span><span>表示任意一个字符，上例中，就是把符合</span><span>r</span><span>与</span><span>o</span><span>之间有两个任意字符的行过滤出来</span><span>。</span>

<span>“*”</span><span>表示零个或多个前面的字符</span><span>。</span>

<span>![13_23.png.jpg](images/13_23.png.jpg)</span>

<span>‘ooo*’</span> <span>表示</span><span>oo, ooo, oooo …</span> <span>或者更多的</span><span>’o’。</span><span>现在你是否想到了</span><span>’.*’</span> <span>这个组合表示什么意义？</span>

<span>![13_24.png.jpg](images/13_24.png.jpg)</span>

<span>‘.*’</span><span>表示零个或多个任意字符，空行也包含在内</span><span>。</span>

<span>**f.** </span><span>**指定要过滤字符出现的次数**</span>

<span>![13_25.png.jpg](images/13_25.png.jpg)</span>

<span>这里用到了</span><span>{ }</span><span>，其内部为数字，表示前面的字符要重复的次数</span><span>。</span><span>上例中表示包含有两个</span><span>o</span> <span>即</span><span>’oo’</span><span>的行</span><span>。</span><span>注意，</span><span>{ }</span><span>左右都需要加上脱意字符</span><span>’\’。</span><span>另外，使用</span><span>{ }</span><span>我们还可以表示一个范围的，具体格式是</span> <span>‘\’</span><span>其中</span><span>n1<n2</span><span>，表示重复</span><span>n1</span><span>到</span><span>n2</span><span>次前面的字符，</span><span>n2</span><span>还可以为空，则表示大于等于</span><span>n1</span><span>次</span><span>。</span>

<span>上面部分讲的</span><span>grep</span><span>，另外笔者常常用到</span><span>egrep</span><span>这个工具，简单点讲，后者是前者的扩展版本，我们可以用</span><span>egrep</span><span>完成</span><span>grep</span><span>不能完成的工作，当然了</span><span>grep</span><span>能完成的</span><span>egrep</span><span>完全可以完成</span><span>。</span><span>如果你嫌麻烦，</span><span>egrep</span><span>了解一下即可，因为</span><span>grep</span><span>的功能已经足够可以胜任你的日常工作了</span><span>。</span><span>下面笔者介绍</span><span>egrep</span><span>不用于</span><span>grep</span><span>的几个用法</span><span>。</span><span>为了试验方便，笔者把</span><span>test.txt</span> <span>编辑成如下内容：</span>

<span>rot:x:0:0:/rot:/bin/bash</span>

<span>operator:x:11:0:operator:/root:/sbin/nologin</span>

<span>operator:x:11:0:operator:/rooot:/sbin/nologin</span>

<span>roooot:x:0:0:/rooooot:/bin/bash</span>

<span>1111111111111111111111111111111</span>

<span>aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa</span>

<span>**a.** </span><span>**筛选一个或一个以上前面的字符**</span>

<span>![13_26.png.jpg](images/13_26.png.jpg)</span>

<span>和</span><span>grep</span> <span>不同的是，</span><span>egrep</span><span>这里是使用</span><span>’+’</span><span>的</span><span>。</span>

<span>**b.** </span><span>**筛选零个或一个前面的字符**</span>

<span>![13_27.png.jpg](images/13_27.png.jpg)</span>

<span>**c.** </span><span>**筛选字符串**</span><span>**1**</span><span>**或者字符串**</span><span>**2**</span>

<span>![13_28.png.jpg](images/13_28.png.jpg)</span>

<span>中间有一个</span><span>’|’</span><span>表示或者的意思，笔者用这个用的很多，所以这个你最好记一下</span><span>。</span>

<span>**d. egrep**</span><span>**中**</span><span>**’( )’**</span><span>**的应用**</span>

<span>![13_29.png.jpg](images/13_29.png.jpg)</span>

<span>用</span><span>’( )’</span><span>表示一个整体，例如</span><span>(oo)+</span><span>就表示</span><span>1</span><span>个</span><span>’oo’</span><span>或者多个</span><span>’oo’</span>

<span>![13_44.png.jpg](images/13_44.png.jpg)</span>

<span>【</span><span>**sed** </span><span>**工具的使用**</span><span>】</span>

<span>grep</span> <span>工具的功能其实还不够强大，其实说白了，</span><span>grep</span><span>实现的只是查找功能，而它却不能实现把查找的内容替换掉</span><span>。</span><span>以前用</span><span>vim</span><span>的时候，可以查找也可以替换，但是只局限于在文本内部来操作，而不能输出到屏幕上</span><span>。sed</span><span>工具以及下面要讲的</span><span>awk</span><span>工具就能实现把替换的文本输出到屏幕上的功能了，而且还有其他更丰富的功能</span><span>。sed</span><span>和</span><span>awk</span><span>都是流式编辑器，是针对文档的行来操作的</span><span>。</span>

<span>**a.** </span><span>**打印某行**</span><span> **sed -n ‘n’p filename** </span><span>**单引号内的**</span><span>**n**</span><span>**是一个数字，表示第几行**</span>

<span>![13_45.png.jpg](images/13_45.png.jpg)</span>

<span>**b.** </span><span>**打印多行**</span><span>**打印整个文档用**</span><span> **-n ‘1,$’p**</span>

<span>![13_46.png.jpg](images/13_46.png.jpg)</span>

<span>**c.** </span><span>**打印包含某个字符串的行**</span>

<span>![13_47.png.jpg](images/13_47.png.jpg)</span>

<span>上面</span><span>grep</span><span>中使用的特殊字符，如</span><span>’^’, ‘$’, ‘.’, ‘*’</span><span>等同样也能在</span><span>sed</span><span>中使用</span><span>。</span>

<span>![13_48.png.jpg](images/13_48.png.jpg)</span>

<span>![13_49.png.jpg](images/13_49.png.jpg)</span>

<span>**d. -e** </span><span>**可以实现多个行为**</span>

<span>![13_50.png.jpg](images/13_50.png.jpg)</span>

<span>**e.** </span><span>**删除某行或者多行**</span>

<span>![13_51.png.jpg](images/13_51.png.jpg)</span>

<span>‘d’</span> <span>这个字符就是删除的动作了，不仅可以删除指定的单行以及多行，而且还可以删除匹配某个字符的行，另外还可以删除从某一行一直到文档末行</span><span>。</span>

<span>![13_52.png.jpg](images/13_52.png.jpg)</span>

<span>**f.** </span><span>**替换字符或字符串**</span>

<span>![13_53.png.jpg](images/13_53.png.jpg)</span>

<span>上例中的</span><span>’s’</span><span>就是替换的命令，</span><span>’g’</span><span>为本行中全局替换，如果不加</span><span>’g’</span><span>，只换该行中出现的第一个</span><span>。</span>

<span>除了可以使用</span><span>’/’</span><span>外，还可以使用其他特殊字符例如</span><span>’#’</span><span>或者</span><span>’@’</span><span>都没有问题</span><span>。</span>

<span>![13_54.png.jpg](images/13_54.png.jpg)</span>

<span>现在思考一下，如何删除文档中的所有数字或者字母？</span>

<span>![13_55.png.jpg](images/13_55.png.jpg)</span>

<span>有意思吧，</span><span>[0-9]</span><span>表示任意的数字</span><span>。</span><span>这里你也可以写成</span><span>[a-zA-Z]</span><span>甚至</span><span>[0-9a-zA-Z]</span>

<span>![13_56.png.jpg](images/13_56.png.jpg)</span>

<span>**g.** </span><span>**调换两个字符串的位置**</span>

<span>![13_57.png.jpg](images/13_57.png.jpg)</span>

<span>这个就需要解释一下了，上例中用</span><span>’()’</span><span>把所想要替换的字符括起来成为一个整体，因为括号在</span><span>sed</span><span>中属于特殊符号，所以需要在前面加脱意字符</span><span>’\’</span><span>，替换时则写成</span><span>’\1’, ‘\2’, ‘\3’</span> <span>的形式</span><span>。</span><span>除了调换两个字符串的位置外，笔者还常常用到在某一行前或者后增加指定内容</span><span>。</span>

<span>![13_78.png.jpg](images/13_78.png.jpg)</span>

<span>**h.** </span><span>**直接修改文件的内容**</span>

<span>sed -i ‘s/:/#/g’ test.txt</span> <span>，这样就可以直接更改</span><span>test.txt</span><span>文件中的内容了</span><span>。</span><span>由于这个命令可以直接把文件修改，所以在修改前最好先复制一下文件以免改错</span><span>。</span>

<span>sed</span><span>常用到的也就上面这些了，只要你多加练习就能熟悉它了</span><span>。</span><span>为了能让你更加牢固的掌握</span><span>sed</span><span>的应用，笔者留几个练习题给你，希望你能认真完成</span><span>。</span>

<span>1\.</span> <span>把</span><span>/etc/passwd</span> <span>复制到</span><span>/root/test.txt</span><span>，用</span><span>sed</span><span>打印所有行；</span>

<span>2\.</span> <span>打印</span><span>test.txt</span><span>的</span><span>3</span><span>到</span><span>10</span><span>行；</span>

<span>3\.</span> <span>打印</span><span>test.txt</span> <span>中包含</span><span>’root’</span><span>的行；</span>

<span>4\.</span> <span>删除</span><span>test.txt</span> <span>的</span><span>15</span><span>行以及以后所有行；</span>

<span>5\.</span> <span>删除</span><span>test.txt</span><span>中包含</span><span>’bash’</span><span>的行；</span>

<span>6\.</span> <span>替换</span><span>test.txt</span> <span>中</span><span>’root’</span><span>为</span><span>’toor’</span><span>；</span>

<span>7\.</span> <span>替换</span><span>test.txt</span><span>中</span><span>’/sbin/nologin’</span><span>为</span><span>’/bin/login’</span>

<span>8\.</span> <span>删除</span><span>test.txt</span><span>中</span><span>5</span><span>到</span><span>10</span><span>行中所有的数字；</span>

<span>9\.</span> <span>删除</span><span>test.txt</span> <span>中所有特殊字符（除了数字以及大小写字母）；</span>

<span>10\.</span> <span>把</span><span>test.txt</span><span>中第一个单词和最后一个单词调换位置；</span>

<span>11\.</span> <span>把</span><span>test.txt</span><span>中出现的第一个数字和最后一个单词替换位置；</span>

<span>12\.</span> <span>把</span><span>test.txt</span> <span>中第一个数字移动到行末尾；</span>

<span>13\.</span> <span>在</span><span>test.txt 20</span><span>行到末行最前面加</span><span>’aaa:’</span><span>；</span>

<span>现在给出以上练习题的答案，你如果实在想不出如何操作，那你看看答案吧，请尽量多想一下</span><span>。</span>

<span>1\. /bin/cp /etc/passwd /root/test.txt ; sed -n '1,/span>p test.txt</span>

<span>2\. sed -n '3,10'p test.txt</span>

<span>3\. sed -n '/root/'p test.txt</span>

<span>4\. sed '15,/span>d test.txt</span>

<span>5\. sed '/bash/'d test.txt</span>

<span>6\. sed 's/root/toor/g' test.txt</span>

<span>7\. sed 's#sbin/nologin#bin/login#g' test.txt</span>

<span>8\. sed '5,10s/[0-9]//g' test.txt</span>

<span>9\. sed 's/[^0-9a-zA-Z]//g' test.txt</span>

<span>10\. sed 's/\(^[a-zA-Z][a-zA-Z]*\)\([^a-zA-Z].*\)\([^a-zA-Z]\)\([a-zA-Z][a-zA-Z]*$\)/\4\2\3\1/' test.txt</span>

<span>11\. sed 's#\([^0-9][^0-9]*\)\([0-9][0-9]*\)\([^0-9].*\)\([^a-zA-Z]\)\([a-zA-Z][a-zA-Z]*$\)#\1\5\3\4\2#' test.txt</span>

<span>12\. sed 's#\([^0-9][^0-9]*\)\([0-9][0-9]*\)\([^0-9].*$\)#\1\3\2#' test.txt</span>

<span>13\. sed '20,$s/^.*$/aaa:&/' test.txt</span>

<span>【</span><span>**awk**</span><span>**工具的使用**</span><span>】</span>

<span>上面也提到了</span><span>awk</span><span>和</span><span>sed</span><span>一样是流式编辑器，它也是针对文档中的行来操作的，一行一行的去执行</span><span>。awk</span><span>比</span><span>sed</span><span>更加强大，它能做到</span><span>sed</span><span>能做到的，同样也能做到</span><span>sed</span><span>不能做到的</span><span>。awk</span><span>工具其实是很复杂的，有专门的书籍来介绍它的应用，但是笔者认为学那么复杂没有必要，只要能处理日常管理工作中的问题即可</span><span>。</span><span>何必让自己的脑袋装那么东西来为难自己？毕竟用的也不多，即使现在教会了你很多，你也学会了，如果很久不用肯定就忘记了</span><span>。</span><span>鉴于此，笔者仅介绍比较常见的</span><span>awk</span><span>应用，如果你感兴趣的话，再去深入研究吧</span><span>。</span>

<span>**a.** </span><span>**截取文档中的某个段**</span>

<span>![13_79.png.jpg](images/13_79.png.jpg)</span>

<span>解释一下，</span><span>-F</span> <span>选项的作用是指定分隔符，如果不加</span><span>-F</span><span>指定，则以空格或者</span><span>tab</span><span>为分隔符</span><span>。</span>

<span>![13_80.png.jpg](images/13_80.png.jpg)</span>

<span>Print</span><span>为打印的动作，用来打印出某个字段</span><span>。$1</span><span>为第一个字段，</span><span>$2</span><span>为第二个字段，依次类推，有一个特殊的那就是</span><span>$0</span><span>，它表示整行</span><span>。</span>

<span>![13_81.png.jpg](images/13_81.png.jpg)</span>

<span>注意</span><span>awk</span><span>的格式，</span><span>-F</span><span>后紧跟单引号，然后里面为分隔符，</span><span>print</span><span>的动作要用</span><span>’{ }’</span><span>括起来，否则会报错</span><span>。print</span><span>还可以打印自定义的内容，但是自定义的内容要用双引号括起来</span><span>。</span>

<span>![13_82.png.jpg](images/13_82.png.jpg)</span>

<span>**b.** </span><span>**匹配字符或字符串**</span>

<span>![13_83.png.jpg](images/13_83.png.jpg)</span>

<span>跟</span><span>sed</span><span>很类似吧，不过还有比</span><span>sed</span><span>更强大的匹配</span><span>。</span>

<span>![13_84.png.jpg](images/13_84.png.jpg)</span>

<span>可以让某个段去匹配，这里的</span><span>’~’</span><span>就是匹配的意思，继续往下看</span>

![13_85.png.jpg](images/13_85.png.jpg)

<span>awk</span><span>还可以多次匹配，如上例中匹配完</span><span>root</span><span>，再匹配</span><span>test</span><span>，它还可以只打印所匹配的段</span><span>。</span>

<span>![13_86.png.jpg](images/13_86.png.jpg)</span>

<span>不过这样没有啥意义，笔者只是为了说明</span><span>awk</span><span>确实比</span><span>sed</span><span>强大</span><span>。</span>

<span>**d.** </span><span>**条件操作符**</span>

<span>![13_87.png.jpg](images/13_87.png.jpg)</span>

<span>awk</span><span>中是可以用逻辑符号判断的，比如</span><span>’==’</span><span>就是等于，也可以理解为</span><span>“</span><span>精确匹配</span><span>”。</span><span>另外也有</span><span>’>’, ‘>=’, ‘<’, ‘<=’, ‘!=’</span> <span>等等，值得注意的是，即使</span><span>$3</span><span>为数字，</span><span>awk</span><span>也不会把它当数字看待，它会认为是一个字符</span><span>。</span><span>所以不要妄图去拿</span><span>$3</span><span>当数字去和数字做比较</span><span>。</span>

<span>![13_88.png.jpg](images/13_88.png.jpg)</span>

<span>这样是得不到我们想要的效果的</span><span>。</span><span>这里只是字符与字符之间的比较，</span><span>’6’</span><span>是</span><span>>’500’</span><span>的</span><span>。</span>

<span>![13_89.png.jpg](images/13_89.png.jpg)</span>

<span>上例中用的是</span><span>’!=’</span> <span>即不匹配</span><span>。</span>

<span>![13_90.png.jpg](images/13_90.png.jpg)</span>

<span>另外还可以使用</span><span>”&&”</span> <span>和</span> <span>“||”</span><span>表示</span><span>“</span><span>并且</span><span>”</span><span>和</span><span>“</span><span>或者</span><span>”</span><span>的意思</span><span>。</span>

<span>![13_91.png.jpg](images/13_91.png.jpg)</span>

<span>也可以是或者的关系</span>

<span>![13_92.png.jpg](images/13_92.png.jpg)</span>

<span>**d. awk**</span><span>**的内置变量**</span>

<span>常用的变量有：</span>

<span>NF</span> <span>：用分隔符分隔后一共有多少段；</span>

<span>NR</span> <span>：行数</span>

<span>![13_93.png.jpg](images/13_93.png.jpg)</span>

<span>上例中，打印总共的段数以及最后一段的值</span><span>。</span>

<span>![13_94.png.jpg](images/13_94.png.jpg)</span>

<span>可以使用</span><span>NR</span><span>作为条件，来打印出指定的行</span><span>。</span>

![13_95.png.jpg](images/13_95.png.jpg)

<span>**e. awk**</span><span>**中的数学运算**</span>

<span>![13_96.png.jpg](images/13_96.png.jpg)</span>

<span>awk</span><span>比较强的地方，还在于能把某个段改成指定的字符串，下面还有更强的呢！</span>

<span>![13_97.png.jpg](images/13_97.png.jpg)</span>

<span>当然还可以计算某个段的总和</span><span>。</span>

<span>![13_101.png.jpg](images/13_101.png.jpg)</span>

<span>这里的</span><span>END</span><span>要注意一下，表示所有的行都已经执行，这是</span><span>awk</span><span>特有的语法，其实</span><span>awk</span><span>连同</span><span>sed</span><span>都可以写成一个脚本文件，而且有他们特有的语法，在</span><span>awk</span><span>中使用</span><span>if</span><span>判断</span><span>、for</span><span>循环都是可以的，只是笔者认为日常管理工作中没有必要使用那么复杂的语句而已</span><span>。</span>

<span>![13_102.png.jpg](images/13_102.png.jpg)</span>

<span>注意这里</span><span>’( )’</span><span>的使用</span><span>。</span>

<span>基本上，正则表达的内容就这些了</span><span>。</span><span>但是笔者要提醒你一下，笔者介绍的这些仅仅是最基本的东西，并没有提啊深入的去讲</span><span>sed</span><span>和</span><span>awk</span><span>，但是完全可以满足日常工作的需要，有时候也许你会碰到比较复杂的需求，如果真遇到了就去请教一下</span><span>google</span><span>吧</span><span>。</span><span>下面出几道关于</span><span>awk</span><span>的练习题，希望你要认真完成</span><span>。</span>

<span>1\.</span> <span>用</span><span>awk</span> <span>打印整个</span><span>test.txt</span> <span>（以下操作都是用</span><span>awk</span><span>工具实现，针对</span><span>test.txt</span><span>）；</span>

<span>2\.</span> <span>查找所有包含</span><span>’bash’</span><span>的行；</span>

<span>3\.</span> <span>用</span><span>’:’</span><span>作为分隔符，查找第三段等于</span><span>0</span><span>的行；</span>

<span>4\.</span> <span>用</span><span>’:’</span><span>作为分隔符，查找第一段为</span><span>’root’</span><span>的行，并把该段的</span><span>’root’</span><span>换成</span><span>’toor’(</span><span>可以连同</span><span>sed</span><span>一起使用</span><span>)</span><span>；</span>

<span>5\.</span> <span>用</span><span>’:’</span><span>作为分隔符，打印最后一段；</span>

<span>6\.</span> <span>打印行数大于</span><span>20</span><span>的所有行；</span>

<span>7\.</span> <span>用</span><span>’:’</span><span>作为分隔符，打印所有第三段小于第四段的行；</span>

<span>8\.</span> <span>用</span><span>’:’</span><span>作为分隔符，打印第一段以及最后一段，并且中间用</span><span>’@’</span><span>连接</span><span>（例如，第一行应该是这样的形式</span> <span>“root@/bin/bash”</span><span>；</span>

<span>9\.</span> <span>用</span><span>’:’</span><span>作为分隔符，把整个文档的第四段相加，求和；</span>

<span>下面给出答案：</span>

<span>1\. awk '' test.txt</span>

<span>2\. awk '/bash/' test.txt</span>

<span>3\. awk -F':' '$3=="0"' test.txt</span>

<span>4\. awk -F':' '$1=="root"' test.txt |sed 's/root/toor/'</span>

<span>5\. awk -F':' '' test.txt</span>

<span>6\. awk -F':' 'NR>20' test.txt</span>

<span>7\. awk -F':' '$3<$4' test.txt</span>

<span>8\. awk -F':' '' test.txt</span>

<span>9\. awk -F':' '{(sum+=$4)}; END ' test.txt</span>
