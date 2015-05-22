# 文档的压缩与打包

<span>在</span><span>windows</span><span>下我们接触最多的压缩文件就是</span><span>.rar</span><span>格式的了</span><span>。</span><span>但在</span><span>linux</span><span>下这样的格式是不能识别的，它有自己所特有的压缩工具</span><span>。</span><span>但有一种文件在</span><span>windows</span><span>和</span><span>linux</span><span>下都能使用那就是</span><span>.zip</span><span>格式的文件了</span><span>。</span><span>压缩的好处不用笔者介绍相信你也晓得吧，它不仅能节省磁盘空间而且在传输的时候还能节省网络带宽呢</span><span>。</span>

<span>在</span><span>linux</span><span>下最常见的压缩文件通常都是以</span><span>.tar.gz</span> <span>为结尾的，除此之外还有</span><span>.tar, .gz, .bz2, .zip</span><span>等等</span><span>。</span><span>以前也介绍过</span><span>linux</span><span>系统中的后缀名其实要不要无所谓，但是对于压缩文件来讲必须要带上</span><span>。</span><span>这是为了判断压缩文件是由哪种压缩工具所压缩，而后才能去正确的解压缩这个文件</span><span>。</span><span>以下介绍常见的后缀名所对应的压缩工具</span><span>。</span>

<span>.gz gzip</span> <span>压缩工具压缩的文件</span>

<span>.bz2 bzip2</span> <span>压缩工具压缩的文件</span>

<span>.tar tar</span> <span>打包程序打包的文件</span><span>(tar</span><span>并没有压缩功能，只是把一个目录合并成一个文件</span><span>)</span>

<span>.tar.gz</span> <span>可以理解为先用</span><span>tar</span><span>打包，然后再</span><span>gzip</span><span>压缩</span>

<span>.tar.bz2</span> <span>同上，先用</span><span>tar</span><span>打包，然后再</span><span>bzip2</span><span>压缩</span>

<span>**【gzip】**</span>

<span>语法：</span> <span>gzip [-d#] filename</span> <span>其中</span><span>#</span><span>为</span><span>1-9</span><span>的数字</span>

<span>-d</span> <span>：解压缩时使用</span>

<span>-#</span> <span>：压缩等级，</span><span>1</span><span>压缩最差，</span><span>9</span><span>压缩最好，</span><span>6</span><span>为默认</span>

<span>![10_1.png.jpg](images/10_1.png.jpg)</span>

<span>压缩</span><span>test.txt</span><span>后，则变成了</span><span>test.txt.gz</span>

<span>![10_7.png.jpg](images/10_7.png.jpg)</span>

<span>用</span><span>-d</span><span>解压缩</span>

<span>要注意的是，</span><span>gzip</span><span>不可以压缩目录</span>

![10_8.png.jpg](images/10_8.png.jpg)

<span>**【bzip2】**</span>

<span>语法：</span><span>bzip2 [-dz] filename</span>

<span>-d</span> <span>：解压缩</span>

<span>-z</span> <span>：压缩</span>

<span>![10_9.png.jpg](images/10_9.png.jpg)</span>

<span>其实</span><span>-z</span><span>参数是可以省略掉的，你不妨试试</span>

<span>![10_10.png.jpg](images/10_10.png.jpg)</span>

<span>跟</span><span>gzip</span><span>的解压类似，也是用</span><span>-d</span><span>解压</span><span>。</span>

<span>**【tar】**</span>

<span>语法：</span><span>tar [-zjxcvfpP] filename</span>

<span>-z</span> <span>：是否同时用</span><span>gzip</span><span>压缩</span>

<span>-j</span> <span>：是否同时用</span><span>bzip2</span><span>压缩</span>

<span>-x</span> <span>：解包或者解压缩</span>

<span>-t</span> <span>：查看</span><span>tar</span><span>包里面的文件</span>

<span>-c</span> <span>：建立一个</span><span>tar</span><span>包或者压缩文件包</span>

<span>-v</span> <span>：可视化</span>

<span>-f</span> <span>：后面跟文件名，压缩时跟</span><span>-f</span><span>文件名，意思是压缩后的文件名为</span><span>filename</span><span>，解压时跟</span><span>-f</span><span>文件名，意思是解压</span><span>filename。</span><span>请注意，如果是多个参数组合的情况下带有</span><span>-f</span><span>，请把</span><span>f</span><span>写到最后面</span><span>。</span>

<span>-p</span> <span>：使用原文件的属性，压缩前什么属性压缩后还什么属性</span><span>。</span><span>（不常用）</span>

<span>-P</span> <span>：可以使用绝对路径</span><span>。</span><span>（不常用）</span>

<span>--exclude filename</span> <span>：在打包或者压缩时，不要将</span><span>filename</span><span>文件包括在内</span><span>。</span><span>（不常用）</span>

<span>![10_11.png.jpg](images/10_11.png.jpg)</span>

<span>首先在</span><span>test</span><span>目录下建立</span><span>test111</span><span>目录，然后在</span><span>test111</span><span>目录下建立</span><span>test2.txt</span><span>，并写入</span><span>”nihao”</span><span>到</span><span>test2.txt</span><span>中，接着是用</span><span>tar</span><span>把</span><span>test111</span><span>打包成</span><span>test111.tar。</span><span>请记住</span><span>-f</span><span>参数后跟的是打包后的文件名</span><span>。</span>

<span>![10_21.png.jpg](images/10_21.png.jpg)</span>

<span>删除原来的</span><span>test111</span><span>目录，然后解包</span><span>test111.tar</span><span>，不管是打包还是解包，原来的文件是不会删除的</span><span>。</span>

<span>![10_22.png.jpg](images/10_22.png.jpg)</span>

<span>打包的同时使用</span><span>gzip</span><span>压缩</span>

<span>![10_23.png.jpg](images/10_23.png.jpg)</span>

<span>用</span><span>-tf</span> <span>跟包名来查看包或者压缩包内的文件都有哪些</span>

<span>![10_24.png.jpg](images/10_24.png.jpg)</span>

<span>先删除</span><span>test111,</span><span>然后用</span><span>tar -zxvf</span> <span>来解压</span><span>.tar.gz</span><span>的压缩包</span><span>。</span>

<span>![10_25.png.jpg](images/10_25.png.jpg)</span>

<span>-jcvf</span> <span>打包的同时用</span><span>bzip2</span><span>压缩，</span><span>-tf</span><span>同样可以查看</span><span>.tar.bz2</span><span>的压缩包</span>

<span>![10_26.png.jpg](images/10_26.png.jpg)</span>

<span>-jxvf</span><span>解压缩</span><span>.tar.bz2</span><span>的压缩包</span>

<span>![10_27.png.jpg](images/10_27.png.jpg)</span>

<span>--exclude</span><span>参数的作用就是打包的时候过滤掉某些文件，如果想过滤多个文件怎么办</span>

<span>![10_28.png.jpg](images/10_28.png.jpg)</span>

<span>只能是继续跟</span> <span>--exclude filename</span><span>了</span><span>。</span>
