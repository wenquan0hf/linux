# 文本编辑工具 vim

<span>前面多次提到过</span><span>vim</span><span>这个东西，它是</span><span>linux</span><span>中必不可少的一个工具</span><span>。</span><span>没有它很多工作都无法完成</span><span>。</span><span>早期的</span><span>Unix</span><span>都是使用的</span><span>vi</span><span>作为系统默认的编辑器的</span><span>。</span><span>你也许会有疑问，</span><span>vi</span><span>与</span><span>vim</span><span>有什么区别？可以这样简单理解，</span><span>vim</span><span>是</span><span>vi</span><span>的升级版</span><span>。</span><span>很多</span><span>linux</span><span>系统管理员都习惯用</span><span>vi</span><span>，那是因为他们接触</span><span>linux</span><span>的时候用的就是</span><span>vi</span><span>，</span><span>vim</span><span>后来才比较流行</span><span>。</span><span>所以，无所谓用</span><span>vi</span><span>和</span><span>vim</span><span>，只要你能达到你想要的目的即可</span><span>。</span>

<span>在笔者看来</span><span>vi</span> <span>和</span><span>vim</span><span>最大的区别就是编辑一个文本时，</span><span>vi</span><span>不会显示颜色，而</span><span>vim</span><span>会显示颜色</span><span>。</span><span>显示颜色更易于用户进行编辑</span><span>。</span><span>其他功能没有什么区别</span><span>。</span><span>所以在</span><span>linux</span><span>系统下，使用</span><span>vi</span><span>还是</span><span>vim</span><span>完全取决你的个人爱好而已</span><span>。</span><span>笔者从一开始学</span><span>linux</span><span>就一直使用</span><span>vim</span><span>，所以也会一直以</span><span>vim</span><span>的角色来教授给你</span><span>。</span>

<span>vim</span><span>的三种模式：一般模式</span><span>、</span><span>编辑模式</span><span>、</span><span>命令模式</span><span>。</span><span>这需要你牢记的，因为以前笔者刚刚从事</span><span>linux</span><span>工作的时候去面试，很多单位的笔试题就有这个知识点</span><span>。</span>

<span>*</span> <span>一般模式：</span><span>当你</span><span>vim filename</span> <span>编辑一个文件时，一进入该文件就是一般模式了</span><span>。</span><span>在这个模式下，你可以做的操作有，上下移动光标；删除某个字符；删除某行；复制</span><span>、</span><span>粘贴一行或者多行</span><span>。</span>

<span>*</span> <span>编辑模式：一般模式下，是不可以修改某一个字符的，只能到编辑模式了</span><span>。</span><span>从一般模式进入编辑模式，只需你按一个键即可（</span><span>i,I,a,A,o,O,r,R</span><span>）</span><span>。</span><span>当进入编辑模式时，会在屏幕的最下一行出现</span><span>“INSERT</span><span>或</span><span>REPLACE”</span><span>的字样</span><span>。</span><span>从编辑模式回到一般模式只需要按一下键盘左上方的</span><span>ESC</span><span>键即可</span><span>。</span>

<span>*</span> <span>命令模式：在一般模式下，输入</span><span>”:”</span><span>或者</span><span>”/”</span><span>即可进入命令模式</span><span>。</span><span>在该模式下，你可以搜索某个字符或者字符串，也可以保存</span><span>、</span><span>替换</span><span>、</span><span>退出</span><span>、</span><span>显示行号等等</span><span>。</span>

<span>下面笔者教你如何在一个空白文档中写入一段文字，然后保存</span><span>。</span>

<span>![9_1.png.jpg](images/9_1.png.jpg)</span>

<span>输入</span><span>vim test.txt</span><span>直接回车进入一般模式</span><span>。</span><span>然后按</span><span>"i"</span> <span>字母进入编辑模式</span>

<span>![9_7.png.jpg](images/9_7.png.jpg)</span>

<span>会看到窗口的左下方出现</span><span>”INSERT”</span><span>字样，说明已经进入了编辑模式，此时就可以写入内容了</span><span>。</span>

<span>![9_8.png.jpg](images/9_8.png.jpg)</span>

<span>等编辑完内容后，按</span><span>ESC</span><span>退出编辑模式，进入一般模式</span><span>。</span><span>此时在左下方的</span><span>”INSERT”</span><span>字样消失，然后按</span><span>”:”</span><span>进入命令模式，最后输入</span><span>wq</span><span>保存并退出</span><span>vim。</span>

<span>![9_9.png.jpg](images/9_9.png.jpg)</span>

<span>这时，看一下</span><span>test.txt</span><span>文档的内容吧</span><span>。</span>

<span>![9_10.png.jpg](images/9_10.png.jpg)</span>

<span>其实</span><span>vim</span><span>为全键盘操作的编辑器，所以在各个模式下都有很多功能键盘的</span><span>。</span><span>下面笔者列举一下，其中笔者认为常用的会用红色标出，需要你多加练习，另外不常用的你也要知道的</span><span>。</span>

| 

<div><span>**一般模式下移动光标**</span></div>

 |

| 

<div><span>h</span><span>或向左方向键</span></div>

 | 

<div><span>光标向左移动一个字符</span></div>

 |
| 

<div><span>j</span><span>或者向下方向键</span></div>

 | 

<div><span>光标向下移动一个字符</span></div>

 |
| 

<div><span>K</span><span>或者向上方向键</span></div>

 | 

<div><span>光标向上移动一个字符</span></div>

 |
| 

<div><span>l</span><span>或者向右方向键</span></div>

 | 

<div><span>光标向右移动一个字符</span></div>

 |
| 

<div><span>Ctrl + f</span> <span>或者</span><span>pageUP</span><span>键</span></div>

 | 

<div><span>屏幕向前移动一页</span></div>

 |
| 

<div><span>Ctrl + b</span> <span>或者</span><span>pageDOWN</span><span>键</span></div>

 | 

<div><span>屏幕向后移动一页</span></div>

 |
| 

<div><span>Ctrl + d</span></div>

 | 

<div><span>屏幕向前移动半页</span></div>

 |
| 

<div><span>Ctrl + u</span></div>

 | 

<div><span>屏幕向后移动半页</span></div>

 |
| 

<div><span>+</span></div>

 | 

<div><span>光标移动到非空格符的下一列</span></div>

 |
| 

<div><span>-</span></div>

 | 

<div><span>光标移动到非空格符的上一列</span></div>

 |
| 

<div><span>n</span><span>空格（</span><span>n</span><span>是数字）</span></div>

 | 

<div><span>按下数字</span><span>n</span><span>然后按空格，则光标向右移动</span><span>n</span><span>个字符，如果该行字符数小于</span><span>n</span><span>，则光标继续从下行开始向右移动，一直到</span><span>n</span></div>

 |
| 

<div><span>0</span><span>（数字</span><span>0</span><span>）或者</span><span>Shift+6</span></div>

 | 

<div><span>移动到本行行首</span></div>

 |
| 

<div><span>Shift+4</span></div>

 | 

<div><span>即</span><span>’$’</span><span>移动到本行行尾</span></div>

 |
| 

<div><span>H</span></div>

 | 

<div><span>光标移动到当前屏幕的最顶行</span></div>

 |
| 

<div><span>M</span></div>

 | 

<div><span>光标移动到当前屏幕的中央那一行</span></div>

 |
| 

<div><span>L</span></div>

 | 

<div><span>光标移动到当前屏幕的最底行</span></div>

 |
| 

<div><span>G</span></div>

 | 

<div><span>光标移动到文本的最末行</span></div>

 |
| 

<div><span>nG</span><span>（</span><span>n</span><span>是数字）</span></div>

 | 

<div><span>移动到该文本的第</span><span>n</span><span>行</span></div>

 |
| 

<div><span>gg</span></div>

 | 

<div><span>移动带该文本的首行</span></div>

 |
| 

<div><span>n</span><span>回车（</span><span>n</span><span>是数字）</span></div>

 | 

<div><span>光标向下移动</span><span>n</span><span>行</span></div>

 |

| 

<div><span>**一般模式下查找与替换**</span></div>

 |

| 

<div><span>/word</span></div>

 | 

<div><span>向光标之后寻找一个字符串名为</span><span>word</span><span>的字符串，当找到第一个</span><span>word</span><span>后，按</span><span>”n”</span><span>继续搜后一个</span></div>

 |
| 

<div><span>?word</span></div>

 | 

<div><span>想光标之前寻找一个字符串名为</span><span>word</span><span>的字符串，当找到第一个</span><span>word</span><span>后，按</span><span>”n”</span><span>继续搜前一个</span></div>

 |
| 

<div><span>:n1,n2s/word1/word2/g</span></div>

 | 

<div><span>在</span><span>n1</span><span>和</span><span>n2</span><span>行间查找</span><span>word1</span><span>这个字符串并替换为</span><span>word2</span><span>，你也可以把</span><span>”/”</span><span>换成</span><span>”#”</span></div>

 |
| 

<div><span>:1,$s/word1/word2/g</span></div>

 | 

<div><span>从第一行到最末行，查找</span><span>word1</span><span>并替换成</span><span>word2</span></div>

 |
| 

<div><span>:1,$s/word1/word2/gc</span></div>

 | 

<div><span>加上</span><span>c</span><span>的作用是，在替换前需要用户确认</span></div>

 |

| 

<div><span>**一般模式下删除**</span><span>**、**</span><span>**复制粘贴**</span></div>

 |

| 

<div><span>x,X</span></div>

 | 

<div><span>x</span><span>为向后删除一个字符，</span><span>X</span><span>为向前删除一个字符</span></div>

 |
| 

<div><span>nx</span><span>（</span><span>n</span><span>为数字）</span></div>

 | 

<div><span>向后删除</span><span>n</span><span>个字符</span></div>

 |
| 

<div><span>dd</span></div>

 | 

<div><span>删除光标所在的那一行</span></div>

 |
| 

<div><span>ndd</span><span>（</span><span>n</span><span>为数字）</span></div>

 | 

<div><span>删除光标所在的向下</span><span>n</span><span>行</span></div>

 |
| 

<div><span>d1G</span></div>

 | 

<div><span>删除光标所在行到第一行的所有数据</span></div>

 |
| 

<div><span>dG</span></div>

 | 

<div><span>删除光标所在行到末行的所有数据</span></div>

 |
| 

<div><span>yy</span></div>

 | 

<div><span>复制光标所在的那行</span></div>

 |
| 

<div><span>nyy</span></div>

 | 

<div><span>复制从光标所在行起向下</span><span>n</span><span>行</span></div>

 |
| 

<div><span>p,P</span></div>

 | 

<div><span>p</span><span>复制的数据从光标下一行粘贴，</span><span>P</span><span>则从光标上一行粘贴</span></div>

 |
| 

<div><span>y1G</span></div>

 | 

<div><span>复制光标所在行到第一行的所有数据</span></div>

 |
| 

<div><span>yG</span></div>

 | 

<div><span>复制光标所在行到末行的所有数据</span></div>

 |
| 

<div><span>J</span></div>

 | 

<div><span>讲光标所在行与下一行的数据结合成同一行</span></div>

 |
| 

<div><span>u</span></div>

 | 

<div><span>还原过去的操作</span></div>

 |

| 

<div><span>**进入编辑模式**</span></div>

 |

| 

<div><span>i</span></div>

 | 

<div><span>在当前字符前插入字符</span></div>

 |
| 

<div><span>I</span></div>

 | 

<div><span>在当前行行首插入字符</span></div>

 |
| 

<div><span>a</span></div>

 | 

<div><span>在当前字符后插入字符</span></div>

 |
| 

<div><span>A</span></div>

 | 

<div><span>在当前行行末插入字符</span></div>

 |
| 

<div><span>o</span></div>

 | 

<div><span>在当前行下插入新的一行</span></div>

 |
| 

<div><span>O</span></div>

 | 

<div><span>在当前行上插入新的一行</span></div>

 |
| 

<div><span>r</span></div>

 | 

<div><span>替换光标所在的字符，只替换一次</span></div>

 |
| 

<div><span>R</span></div>

 | 

<div><span>一直替换光标所在的字符，一直到按下</span><span>ESC</span></div>

 |

| 

<div><span>**命令模式**</span></div>

 |

| 

<div><span>:w</span></div>

 | 

<div><span>将编辑过的文本保存</span></div>

 |
| 

<div><span>:w!</span></div>

 | 

<div><span>若文本属性为只读时，强制保存</span></div>

 |
| 

<div><span>:q</span></div>

 | 

<div><span>退出</span><span>vim</span></div>

 |
| 

<div><span>:q!</span></div>

 | 

<div><span>不管编辑或未编辑都不保存退出</span></div>

 |
| 

<div><span>:wq</span></div>

 | 

<div><span>保存，退出</span></div>

 |
| 

<div><span>:e!</span></div>

 | 

<div><span>将文档还原成最原始状态</span></div>

 |
| 

<div><span>ZZ</span></div>

 | 

<div><span>若文档没有改动，则不储存离开，若文档改动过，则储存后离开，等同于</span><span>:wq</span></div>

 |
| 

<div><span>:w [filename]</span></div>

 | 

<div><span>编辑后的文档另存为</span><span>filename</span></div>

 |
| 

<div><span>:r [filename]</span></div>

 | 

<div><span>在当前光标所在行的下面读入</span><span>filename</span><span>文档的内容</span></div>

 |
| 

<div><span>:set nu</span></div>

 | 

<div><span>在每行的行首显示行号</span></div>

 |
| 

<div><span>:set nonu</span></div>

 | 

<div><span>取消行号</span></div>

 |
| 

<div><span>n1,n2 w [filename]</span></div>

 | 

<div><span>将</span><span>n1</span><span>到</span><span>n2</span><span>的内容另存为</span><span>filename</span><span>这个文档</span></div>

 |
| 

<div><span>:! command</span></div>

 | 

<div><span>暂时离开</span><span>vim</span><span>运行某个</span><span>linux</span><span>命令，例如</span> <span>:! ls /home</span> <span>暂时列出</span><span>/home</span><span>目录下的文件，然后会提示按回车回到</span><span>vim</span></div>

 |

<span>暂时就讲这么多了</span><span>。</span><span>如果你全部掌握，你就是</span><span>vim</span><span>高手啦</span><span>。</span><span>如果你觉得太多，只要记住笔者标红部分即可，其他的用时再过来查就</span><span>ok</span><span>啦</span><span>。</span><span>下面笔者给你留一个小作业，希望你要认真完成！</span>

<span>1\.</span> <span>请把</span><span>/etc/init.d/iptables</span> <span>复制到</span><span>/root/</span><span>目录下，并重命名为</span><span>test.txt</span>

<span>2\.</span> <span>用</span><span>vim</span><span>打开</span><span>test.txt</span><span>并设置行号</span>

<span>3\.</span> <span>分别向下</span><span>、</span><span>向右</span><span>、</span><span>向左</span><span>、</span><span>向右移动</span><span>5</span><span>个字符</span>

<span>4\.</span> <span>分别向下</span><span>、</span><span>向上翻两页</span>

<span>5\.</span> <span>把光标移动到第</span><span>49</span><span>行</span>

<span>6\.</span> <span>让光标移动到行末，再移动到行首</span>

<span>7\.</span> <span>移动到</span><span>test.txt</span><span>文件的最后一行</span>

<span>8\.</span> <span>移动到文件的首行</span>

<span>9\.</span> <span>搜索文件中出现的</span> <span>iptables</span> <span>并数一下一共出现多少个</span>

<span>10\.</span> <span>把从第一行到第三行出现的</span><span>iptables</span> <span>替换成</span><span>iptable</span>

<span>11\.</span> <span>还原上一步操作</span>

<span>12\.</span> <span>把整个文件中所有的</span><span>iptables</span><span>替换成</span><span>iptable</span>

<span>13\.</span> <span>把光标移动到</span><span>50</span><span>行，删除字符</span><span>”$”</span>

<span>14\.</span> <span>还原上一步操作</span>

<span>15\.</span> <span>删除第</span><span>50</span><span>行</span>

<span>16\.</span> <span>还原上一步操作</span>

<span>17\.</span> <span>删除从</span><span>37</span><span>行到</span><span>42</span><span>行的所有内容</span>

<span>18\.</span> <span>还原上一步操作</span>

<span>19\.</span> <span>复制</span><span>48</span><span>行并粘贴到</span><span>52</span><span>行下面</span>

<span>20\.</span> <span>还原上一步操作（按两次</span><span>u</span><span>）</span>

<span>21\.</span> <span>复制从</span><span>37</span><span>行到</span><span>42</span><span>行的内容并粘贴到</span><span>44</span><span>行上面</span>

<span>23\.</span> <span>还原上一步操作（按两次</span><span>u</span><span>）</span>

<span>24\.</span> <span>把</span><span>37</span><span>行到</span><span>42</span><span>行的内容移动到</span><span>19</span><span>行下面</span>

<span>25\.</span> <span>还原上一步操作（按两次</span><span>u</span><span>）</span>

<span>26\.</span> <span>光标移动到首行，把</span><span>/bin/sh</span> <span>改成</span> <span>/bin/bash</span>

<span>27\.</span> <span>在第一行下面插入新的一行，并输入</span><span>”# Hello!”</span>

<span>28\.</span> <span>保存文档并退出</span>
