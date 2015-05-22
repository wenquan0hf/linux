# Linux 磁盘管理 

<span>【</span><span>**查看磁盘或者目录的容量**</span><span> **df** </span><span>**和**</span><span> **du**</span><span>】</span>

<span>**df** </span><span>查看已挂载磁盘的总容量</span><span>、</span><span>使用容量</span><span>、</span><span>剩余容量等，可以不加任何参数，默认是按</span><span>k</span><span>为单位显示的</span>

<span>![8_1.png.jpg](images/8_1.png.jpg)</span>

<span>df</span><span>常用参数有</span> <span>–i -h -k –m</span><span>等</span>

<span>-i</span> <span>使用</span><span>inodes</span> <span>显示结果</span>

<span>![8_12.png.jpg](images/8_12.png.jpg)</span>

<span>-h</span> <span>使用合适的单位显示，例如</span><span>G</span>

<span>![8_13.png.jpg](images/8_13.png.jpg)</span>

<span>-k -m</span> <span>分别为使用</span><span>K</span><span>，</span><span>M</span><span>为单位显示</span>

<span>![8_14.png.jpg](images/8_14.png.jpg)</span>

<span>简单介绍一下，你看到的相关数据</span><span>。Filesystem</span> <span>表示扇区，也就是你划分磁盘时所分的区；</span><span>1K-blocks/1M-blocks</span><span>表示以</span><span>1K/1M</span><span>为单位；</span><span>Used</span> <span>和</span> <span>Available</span> <span>分别是已使用和剩余；</span><span>Use%</span> <span>就是已经使用的百分比，如果这个值大于</span><span>90%</span> <span>那么你就应该注意了，磁盘很有可能马上就会变满的；</span><span>Mounted on</span> <span>则表示该分区（扇区）所挂载的地方</span><span>。</span>

<span>**du** </span><span>**用来查看某个目录所占空间大小**</span>

<span>语法：</span><span>du [-abckmsh] [</span><span>文件或者目录名</span><span>]</span> <span>常用的参数有：</span>

<span>-a</span><span>：全部文件与目录大小都列出来</span><span>。</span><span>如果不加任何选项和参数只列出目录（包含子目录）大小</span><span>。</span>

<span>![8_15.png.jpg](images/8_15.png.jpg)</span>

<span>-b</span><span>：列出的值以</span><span>bytes</span><span>为单位输出，默认是以</span><span>Kbytes</span>

<span>![8_16.png.jpg](images/8_16.png.jpg)</span>

<span>-c</span><span>：最后加总</span>

<span>![8_17.png.jpg](images/8_17.png.jpg)</span>

<span>-k</span><span>：以</span><span>KB</span><span>为单位输出</span>

<span>-m</span><span>：以</span><span>MB</span><span>为单位输出</span>

<span>-s</span><span>：只列出总和</span>

<span>-h</span><span>：系统自动调节单位，例如文件太小可能就几</span><span>K</span><span>，那么就以</span><span>K</span><span>为单位显示，如果大到几</span><span>G</span><span>，则就以</span><span>G</span><span>为单位显示</span><span>。</span><span>笔者习惯用</span> <span>du –sh filename</span> <span>这样的形式</span><span>。</span>

<span>![8_18.png.jpg](images/8_18.png.jpg)</span>

<span>**【**</span><span>**磁盘的分区和格式化**</span><span>**】**</span>

<span>笔者经常做的事情就是拿一个全新的磁盘来分区并格式化</span><span>。</span><span>这也说明了作为一个</span><span>linux</span><span>系统管理员，对于磁盘的操作必须要熟练</span><span>。</span><span>所以请你认真学习该部分内容</span><span>。</span>

<span>fdisk linux</span><span>下的硬盘分区工具</span>

<span>语法：</span> <span>fdisk [-l ] [</span><span>设备名称</span><span>]</span>

<span>-l</span> <span>：后边不跟设备名会直接列出系统中所有的磁盘设备以及分区表，加上设备名会列出该设备的分区表</span><span>。</span>

<span>![8_19.png.jpg](images/8_19.png.jpg)</span>

<span>![8_20.png.jpg](images/8_20.png.jpg)</span>

<span>如果不加</span><span>-l</span> <span>则进入另一个模式，在该模式下，可以对磁盘进行分区操作</span><span>。</span>

<span>![8_21.png.jpg](images/8_21.png.jpg)</span>

<span>刚进入该模式下，会有一个提示</span><span>Command (m for help):</span> <span>此时按</span><span>m</span><span>则会打印出帮助列表，如果你英文好，我想你不难理解这些字母的功能</span><span>。</span><span>笔者常用的有</span><span>p, n,d, w, q.</span>

<span>P</span><span>：打印当前磁盘的分区情况</span><span>。</span>

<span>![8_29.png.jpg](images/8_29.png.jpg)</span>

<span>n</span><span>：重新建立一个新的分区</span><span>。</span>

<span>w</span><span>：保存操作</span><span>。</span>

<span>q</span><span>：退出</span><span>。</span>

<span>d</span><span>：删除一个分区</span>

<span>因为笔者的</span><span>linux</span><span>系统是安装在虚拟机上的，所以我可以增加一块新的磁盘</span><span>。</span><span>然后笔者会把新的磁盘分成多个分区</span><span>。</span>

<span>![8_30.png.jpg](images/8_30.png.jpg)</span>

<span>当再次</span><span>fdisk -l</span> <span>查看时发现多了一个</span><span>/dev/hdb</span> <span>设备，并提示该设备没有可用的分区表</span><span>。</span><span>那么下面就来分一下这个</span><span>/dev/hdb.</span>

<span>![8_31.png.jpg](images/8_31.png.jpg)</span>

<span>首先用</span><span>p</span><span>查看一下，并没有任何分区信息</span><span>。</span>

<span>![8_32.png.jpg](images/8_32.png.jpg)</span>

<span>用</span><span>n</span><span>创建一个新的分区，会提示要建立</span><span>e</span> <span>（</span><span>extended</span> <span>扩展分区）或者</span><span>p</span> <span>（</span><span>primary partition</span><span>主分区），这里笔者选择主分区，所以按了</span><span>p</span><span>回车后，又让输入</span><span>First cylinder</span> <span>你或者直接回车或者输入一个数字，因为这块磁盘是新的并没有任何分区，所以直接回车其实就是从</span><span>1</span><span>开始了</span><span>。</span><span>你也可以自定义输入，但不要超过</span><span>2080</span><span>，笔者这里输入</span><span>1</span><span>回车</span><span>。</span><span>此时会提示要分多大，可以写一个数值（</span><span>2-2080</span><span>），也可以输入</span><span>+sizeK</span><span>或者</span><span>+sizeM</span><span>，后者比较直观容易理解，所以笔者在这里输入</span><span>+100M</span><span>，即我分了一个</span><span>100M</span><span>的主分区</span><span>。</span><span>再用</span><span>p</span><span>查看时，果真多出来一个分区</span><span>。</span><span>然后笔者继续重复前面的操作，建立了</span><span>4</span><span>个主分区</span><span>。</span><span>当笔者再次输入</span><span>n</span><span>创建分区时，结果提示错了</span><span>。</span>

<span>![8_33.png.jpg](images/8_33.png.jpg)</span>

<span>由此你会发现，在</span><span>linux</span><span>中最多只能创建</span><span>4</span><span>个主分区，那如果你想多创建几个分区如何做？很容易，在创建完第三个分区后，创建第四个分区时选择扩展分区</span><span>。</span>

<span>![8_34.png.jpg](images/8_34.png.jpg)</span><span>先删除第四个主分区，然后建立一个扩展分区</span>

<span>![8_35.png.jpg](images/8_35.png.jpg)</span>

<span>在建立扩展分区时，会问你要分多少给这个扩展分区，笔者直接回车，即把所有空间都分给了这个扩展分区</span><span>。</span><span>这个扩展分区</span><span>/dev/hdb4</span><span>并不能往里写数据，它只是一个空壳子，需要我们继续在这个空壳中继续创建分区</span><span>。</span>

<span>![8_83.png.jpg](images/8_83.png.jpg)</span>

<span>当建立完扩展分区，然后按</span><span>n</span><span>创建新分区时你会发现不再提示是要建立</span><span>p</span><span>还是</span><span>e</span><span>了，因为我们已经不能再创建</span><span>p</span><span>了</span><span>。</span><span>在这里需要你明白的是，</span><span>hdb5</span> <span>其实只是</span> <span>hdb4</span> <span>中的一个子分区，到目前为止可用的分区也才</span><span>4</span><span>个，那笔者就再创建第</span><span>5</span><span>个分区出来</span><span>。</span>

<span>![8_84.png.jpg](images/8_84.png.jpg)</span>

<span>然后按</span><span>w</span><span>保存，该模式自动退出，如果你不想保存分区信息直接按</span><span>q</span><span>即可退出</span><span>。</span>

<span>![8_85.png.jpg](images/8_85.png.jpg)</span>

<span>下面我们把刚分好的分区删除，重新建立分区</span><span>。</span><span>如何删除你还记得吧，对了就是直接按</span><span>d</span><span>然后选择合适的数字</span><span>。</span><span>删除完所有分区后，这块磁盘就恢复如初了</span><span>。</span>

<span>![8_86.png.jpg](images/8_86.png.jpg)</span>

<span>![8_87.png.jpg](images/8_87.png.jpg)</span>

<span>第一个分区，我们就建立成扩展分区</span><span>。</span><span>并且分给它</span><span>200M。</span>

<span>![8_88.png.jpg](images/8_88.png.jpg)</span>

<span>当再次新建分区时，发生了变化，不再是</span><span>p</span><span>或者</span><span>e</span><span>了，而是</span><span>p</span><span>或者</span><span>l</span><span>（逻辑分区），这是为什么呢？在上面也提到了，一个扩展分区只是一个空壳，在扩展分区下才可以继续划分小的分区，这个小的分区其实就是逻辑分区了</span><span>。</span>

<span>![8_89.png.jpg](images/8_89.png.jpg)</span>

<span>而且这个逻辑分区默认都是从字数</span><span>5</span><span>开始的，因为前面的数字要么给主分区留着，要么给扩展分区留着</span><span>。</span><span>由此我们也可以得到，在</span><span>linux</span><span>中最多可以创建</span><span>4</span><span>个主分区，一旦创建</span><span>4</span><span>个主分区后就不能增加任何分区了</span><span>。</span><span>另外最多也只能创建一个扩展分区</span><span>。</span><span>扩展分区下的逻辑分区最多可以创建多少呢？</span><span>IDE</span><span>的硬盘（类似于</span><span>hda, hdb, hdc</span> <span>等）最多可以创建</span><span>10</span><span>个（</span><span>hdb5-hdb15</span><span>），这是笔者试验出来的结果</span><span>。</span><span>有的资料说</span><span>linux</span><span>下的逻辑分区是没有限制的，也有的说最大可以到</span><span>64</span><span>，至于对不对，需要你去近一步考察了，我们没有必要多么深入的研究这个问题，也没有什么意义</span><span>。</span>

<span>通过以上操作，相信你也学会了用</span><span>fdisk</span> <span>来分区了吧</span><span>。</span><span>值得提出的是，不要闲着没事分区玩儿，这操作的危险性是很高的，一不留神就把你服务器上的数据全部给分没有了</span><span>。</span><span>如果有分区的操作，那么请保持百分之二百的细心，切记切记！</span>

<span>**mkfs.ext2 / mkfs.ext3 /mke2fs** </span><span>**格式化**</span><span>**linux**</span><span>**硬盘分区**</span>

<span>当用</span><span>man</span><span>查询这三个命令的帮助文档时，你会发现我们看到了同一个帮助文档，这说明三个命令是一样的</span><span>。</span><span>常用的选项有：</span>

<span>-b</span><span>：分区时设定每个数据区块占用空间大小，目前支持</span><span>1024, 2048</span> <span>以及</span><span>4096 bytes</span><span>每个块</span><span>。</span>

<span>-i</span><span>：设定</span><span>inode</span><span>大小</span>

<span>-N</span><span>：设定</span><span>inode</span><span>数量，有时使用默认的inode数不够用，所以要自定设定inode数量。</span>

<span>-c</span><span>：在格式化前先检测一下磁盘是否有问题，加上这个选项后会非常慢</span>

<span>-L</span><span>：预设该分区的标签</span><span>label</span>

<span>-j</span><span>：建立</span><span>ext3</span><span>格式的分区，如果使用</span><span>mkfs.ext3</span> <span>就不用加这个选项了</span>

<span>![8_90.png.jpg](images/8_90.png.jpg)</span>

<span>不加任何选项，直接格式化</span><span>/dev/hdb1</span>

<span>![8_91.png.jpg](images/8_91.png.jpg)</span>

<span>上例中更改了</span><span>block size</span><span>为</span><span>4096</span> <span>默认是</span><span>1024</span><span>，而</span><span>inode大小</span><span>设定为</span><span>4096。</span>

<span>下面的例子分区时自定义分区的</span><span>label</span><span>（标签）名</span><span>。</span>

<span>![8_92.png.jpg](images/8_92.png.jpg)</span>

<span>**e2label** </span><span>**用来查看或者修改分区的标签（**</span><span>**label**</span><span>**）**</span>

<span>这个命令很简单，后边直接跟分区编号，即可查看该分区的</span><span>label</span><span>，当想要修改标签名时，分区编号后边跟想要的标签名即可</span><span>。</span>

<span>![8_93.png.jpg](images/8_93.png.jpg)</span>

<span>**fsck** </span><span>**检查硬盘有没有坏道**</span>

<span>语法：</span> <span>fsck [-Aar] [</span><span>分区</span><span>]</span>

<span>-A</span> <span>：加该参数时，后不需要跟分区名作为参数</span><span>。</span><span>它会自动检查</span><span>/etc/fstab</span> <span>文件下的所有分区（开机过程中就会执行一次该操作）；</span>

<span>-a</span> <span>：自动修复检查到有问题的分区；</span>

<span>-r</span> <span>：当检查到有坏道的分区时会让用户决定是否修复</span><span>。</span>

<span>![8_94.png.jpg](images/8_94.png.jpg)</span>

<span>当你使用</span><span>fsck</span><span>检查磁盘有无坏道时，会提示用户</span><span>“</span><span>跑这个任务可能会导致某些挂载的文件系统损坏</span><span>”</span><span>，所以这个命令不要轻易运行</span><span>。</span><span>否则真的遇到问题，系统甚至都不能启动了</span><span>。</span>

<span>![8_95.png.jpg](images/8_95.png.jpg)</span>

<span>**【**</span><span>**挂载**</span><span>**/**</span><span>**卸载磁盘**</span><span>**】**</span>

<span>在上面的内容中讲到了磁盘的分区和格式化，那么格式化完了后，如何去用它呢？这就涉及到了挂载这块磁盘</span><span>。</span><span>格式化后的磁盘其实是一个块设备文件，类型为</span><span>b</span><span>，也许你会想，既然这个块文件就是那个分区，那么直接在那个文件中写数据不就写到了那个分区中么？当然不行</span><span>。</span>

<span>在挂载某个分区前需要先建立一个挂载点，这个挂载点是以目录的形式出现的</span><span>。</span><span>一旦把某一个分区挂载到了这个挂载点（目录）下，那么再往这个目录写数据使，则都会写到该分区中</span><span>。</span><span>这就需要你注意一下，在挂载该分区前，挂载点（目录）下必须是个空目录</span><span>。</span><span>其实目录不为空并不影响所挂载分区的使用，但是一旦挂载上了，那么该目录下以前的东西就不能看到了</span><span>。</span><span>只有卸载掉该分区后才能看到</span><span>。</span>

<span>**mount** </span><span>**挂载设备**</span>

<span>![8_96.png.jpg](images/8_96.png.jpg)</span>

<span>先建立</span><span>/test1 /test2</span> <span>目录，然后在</span><span>/test1</span><span>目录下建立一个</span><span>1.txt</span><span>文件</span><span>。</span>

<span>![8_97.png.jpg](images/8_97.png.jpg)</span>

<span>把</span><span>/dev/hdb1</span><span>分区挂载到</span><span>/test1</span><span>目录，然后再查看</span><span>/test1</span><span>目录发下，</span><span>1.txt</span><span>不存在了</span><span>。</span><span>此时往</span><span>/test1</span><span>目录下写数据，则会写到</span><span>/dev/hdb1</span><span>分区中</span><span>。</span><span>在讲</span><span>mount</span><span>的</span><span>-a</span><span>选项时，我们有必要先了解一下这个文件</span> <span>/etc/fstab</span>

<span>![8_98.png.jpg](images/8_98.png.jpg)</span>

<span>这个文件是系统启动时，需要挂载的各个分区</span><span>。</span><span>第一列就是分区的</span><span>label</span><span>；第二列是挂载点；第三列是分区的格式；第四列则是</span><span>mount</span><span>的一些挂载参数，等下会详细介绍一下有哪些参数，一般情况下，直接写</span><span>defaults</span><span>即可；第五列的数字表示是否被</span><span>dump</span><span>备份，是的话这里就是</span><span>1</span><span>，否则就是</span><span>0</span><span>；第六列是开机时是否自检磁盘，就是刚才讲过的那个</span><span>fsck</span><span>检测</span><span>。1</span><span>，</span><span>2</span><span>都表示检测，</span><span>0</span><span>表示不检测，在</span><span>Redhat</span><span>中，这个</span><span>1</span><span>，</span><span>2</span><span>还有个说法，</span><span>/</span> <span>分区必须设为</span><span>1</span><span>，而且整个</span><span>fstab</span><span>中只允许出现一个</span><span>1</span><span>，这里有一个优先级的说法</span><span>。1</span><span>比</span><span>2</span><span>优先级高，所以先检测</span><span>1</span><span>，然后再检测</span><span>2</span><span>，如果有多个分区需要开机检测那么都设置成</span><span>2</span><span>吧，</span><span>1</span><span>检测完了后会同时去检测</span><span>2。</span><span>下面该说说第四列中常用到的参数了</span><span>。</span>

<span>async/sync</span> <span>：</span><span>async</span><span>表示和磁盘和内存不同步，系统每隔一段时间把内存数据写入磁盘中，而</span><span>sync</span><span>则会时时同步内存和磁盘中数据；</span>

<span>auto/noauto</span> <span>：开机自动挂载</span><span>/</span><span>不自动挂载；</span>

<span>default</span><span>：按照大多数永久文件系统的缺省值设置挂载定义，它包含了</span><span>rw, suid, dev, exec, auto, nouser,async</span> <span>；</span>

<span>ro</span><span>：按只读权限挂载</span><span>；</span>

<span>rw</span><span>：按可读可写权限挂载</span><span>；</span>

<span>exec/noexec</span> <span>：允许</span><span>/</span><span>不允许可执行文件执行，但千万不要把根分区挂载为</span><span>noexec</span><span>，那就无法使用系统了，连</span><span>mount</span><span>命令都无法使用了，这时只有重新做系统了；</span>

<span>user/nouser</span> <span>：允许</span><span>/</span><span>不允许</span><span>root</span><span>外的其他用户挂载分区，为了安全考虑，请用</span><span>nouser</span> <span>；</span>

<span>suid/nosuid</span> <span>：允许</span><span>/</span><span>不允许分区有</span><span>suid</span><span>属性，一般设置</span><span>nosuid</span> <span>；</span>

<span>usrquota</span> <span>：启动使用者磁盘配额模式，磁盘配额相关内容在后续章节会做介绍；</span>

<span>grquota</span> <span>：启动群组磁盘配额模式；</span>

<span>学完这个</span><span>/etc/fstab</span><span>后，我们就可以自己修改这个文件，增加一行来挂载新增分区</span><span>。</span><span>例如，笔者增加了这样一行</span>

<span>/dev/hdb1 /test1 ext3 defaults 0 0</span>

<span>那么系统再重启时就会挂载这个分区了</span><span>。</span>

<span>讲完了</span><span>/etc/fstab</span> <span>我们继续回来讲这个</span><span>mount</span><span>，</span><span>mout -a</span> <span>如果运行了这个命令，则会把</span><span>/etc/fstab</span><span>中出现的所有磁盘分区挂载上</span><span>。</span><span>所以当你在</span><span>/etc/fstab</span><span>文件中增加一行后，你完全可以直接运行</span><span>mount -a</span> <span>来挂载你增加的那行，这样就不用重启啦</span><span>。</span>

<span>你可以使用</span><span>mount -o</span> <span>选项来重新挂载一个分区，并同时指定你想要的选项（即上边介绍</span><span>fstab</span><span>第六列中那些）</span>

<span>![8_99.png.jpg](images/8_99.png.jpg)</span>

<span>看到了吧，使用了</span><span>ro</span><span>选项，则不能新建文件了</span><span>。</span>

<span>![8_100.png.jpg](images/8_100.png.jpg)</span>

<span>再重新挂载一次就恢复正常了，如果不加任何其他选项，则就是</span><span>defaults。</span>

<span>笔者在日常的运维工作中遇到过这样的情况，一台服务器上新装了亮块磁盘，磁盘</span><span>a</span><span>（在服务器上显示为</span><span>sdc</span><span>）和磁盘</span><span>b</span><span>（在服务器上显示为</span><span>sdd</span><span>），有一次把这两块磁盘都拔掉了，然后再重新插上，重启机器，结果磁盘编号调换了，</span><span>a</span><span>变成了</span><span>sdd</span><span>，</span><span>b</span><span>变成了</span><span>sdc</span><span>（这是因为把磁盘插错了插槽），问题来了</span><span>。</span><span>通过上边的学习，你挂载磁盘是通过</span><span>/dev/hdb1</span> <span>这样的分区名字来挂载的，如果先前加入到了</span><span>/etc/fstab</span> <span>中，结果系统启动后则会挂载错分区</span><span>。</span><span>那么怎么样避免这样的情况发生？</span>

<span>**blkid** </span><span>这个命令是用来显示磁盘分区</span><span>uuid</span><span>的，</span><span>uuid</span><span>其实就是一大串字符，在</span><span>linux</span><span>系统中每一个分区都会有唯一的一个</span><span>uuid。</span><span>说到这，聪明的你想到了吧，没有错，我们就用这唯一的</span><span>uuid</span><span>来挂载磁盘分区</span><span>。</span>

<span>![8_101.png.jpg](images/8_101.png.jpg)</span>

<span>这个命令笔者只是用来显示</span><span>uuid</span><span>，没有其他用途所以不做详细介绍，当然你也可以在命令后边跟某一个分区，只显示该分区的</span><span>uuid。</span>

<span>![8_102.png.jpg](images/8_102.png.jpg)</span>

<span>看到了吧，其实是很好用的</span><span>。</span><span>那么怎么让它也开机启动？很简单，把刚才敲的</span><span>mount</span> <span>磁盘的命令直接写到</span> <span>/etc/rc.d/rc.local</span> <span>文件即可</span><span>。</span><span>对了，笔者到现在还没有给你讲过这个</span><span>rc.local</span><span>文件的作用</span><span>。</span><span>简单点说，系统启动完后会执行这个文件中的命令</span><span>。</span><span>所以只要你想开机后运行什么命令统统写入到这个文件下面吧</span><span>。</span>

<span>![8_103.png.jpg](images/8_103.png.jpg)</span>

<span>其实这个文件就是一个</span><span>shell</span> <span>脚本，以后笔者会单独用一章来介绍它</span><span>。</span><span>行开头的</span><span>”#”</span><span>是注释的意思，代表这行在这个脚本中不生效</span><span>。</span><span>你想让系统开机后运行什么命令，就把什么命令写到这里面来</span><span>。</span><span>就比如刚才笔者挂载的那条命令</span><span>。</span><span>你可以这样实现：</span>

<span>![8_104.png.jpg](images/8_104.png.jpg)</span>

<span>mount</span> <span>还有一个比较常用的选项就是</span><span>-t</span> <span>，后边指定文件系统的类型，比如挂载软盘时就需要指定</span> <span>vfat</span><span>，而挂载光盘时就需要指定</span><span>iso9660</span><span>，但在笔者多年来的经验，目前的系统都是智能识别所要挂载分区的系统格式类别的</span><span>。</span><span>也就是说，用不着你去指定，它会自动判断的</span><span>。</span>

<span>![8_105.png.jpg](images/8_105.png.jpg)</span>

<span>**umount** </span><span>**卸载设备**</span>

<span>现在你学会了如何挂载一个设备，那么如何去卸载一个设备呢，这就要用到</span><span>umount</span><span>了，这个命令也简单的很，后边可以跟挂载点，也可以跟分区名</span><span>(/dev/hdb1)</span>

![8_106.png.jpg](images/8_106.png.jpg)

<span>有时也许你会遇到比较难卸载的设备，就像在</span><span>windows</span><span>下无法删除</span><span>U</span><span>盘一样，教你一个特管用的方法就是</span> <span>umount -l /dev/hdb1</span> <span>，这个</span><span>-l</span><span>选项有强制卸载的意思，你一定要记住哦，非常有用的</span><span>。</span>

<span>**【**</span><span>**建立一个**</span><span>**swap**</span><span>**文件**</span><span>**】**</span>

<span>从装系统时就接触过这个</span><span>swap</span><span>了，前面也说过它类似与</span><span>windows</span><span>的虚拟内存，分区的时候一般大小为内存的</span><span>2</span><span>倍，如果你的内存超过</span><span>4G</span><span>，那么你分</span><span>8G</span><span>似乎是没有必要了</span><span>。</span><span>分</span><span>4G</span><span>足够日常交换了</span><span>。</span><span>然而，还会有虚拟内存不够用的情况发生</span><span>。</span><span>如果真遇到了，莫非还要重新分一下磁盘？当然不能！那我们就增加一个虚拟的磁盘出来</span><span>。</span>

<span>基本的思路就是：建立</span><span>swapfile</span> <span></span><span>格式化为</span><span>swap</span><span>格式</span><span></span><span>启用该虚拟磁盘</span>

<span>![8_107.png.jpg](images/8_107.png.jpg)</span>

<span>利用</span><span>dd</span> <span>来创建一个</span><span>419M</span><span>的文件</span><span>/tmp/newdisk</span><span>出来，其中</span><span>if</span><span>代表从哪个文件读，</span><span>/dev/zero</span><span>是</span><span>linux</span><span>下特有的一个</span><span>0</span><span>生成器，</span><span>of</span><span>表示输出到哪个文件，</span><span>bs</span><span>即块大小，</span><span>count</span><span>则定义有多少个块</span><span>。</span>

<span>![8_108.png.jpg](images/8_108.png.jpg)</span>

<span>mkswap</span> <span>这个命令是专门格式化</span><span>swap</span><span>格式的分区的，这个命令用的时候一定要看清楚了，否则把其他分区给格式化错了就只有哭了</span><span>。</span>

<span>![8_109.png.jpg](images/8_109.png.jpg)</span>

<span>free</span> <span>是用来查看系统内存以及虚拟内存使用情况的，</span><span>-m</span><span>选项是以</span><span>M</span><span>的形式查看</span><span>。</span><span>可以看到当前系统的</span><span>。</span><span>而</span><span>swapon</span> <span>是启用我们新建的</span><span>swap</span><span>文件，启用后再用</span><span>free</span><span>查看发现多了</span><span>400M。</span>

<span>![8_110.png.jpg](images/8_110.png.jpg)</span>

<span>我们还可以用</span><span>swapoff</span> <span>关闭启用的</span><span>swap</span><span>文件</span><span>。</span>

<span>**【**</span><span>**磁盘配额**</span><span>**】**</span>

<span>磁盘配合其实就是给每个用户分配一定的磁盘额度，只允许他使用这个额度范围内的磁盘空间</span><span>。</span><span>在</span><span>linux</span><span>系统中，是多用户多任务的环境，所以会有很多人共用一个磁盘的情况</span><span>。</span><span>针对每个用户去限定一定量的磁盘空间是有必要的，这样才显得公平</span><span>。</span>

<span>在</span><span>linux</span><span>中，用来管理磁盘配额的东西就是</span><span>quota</span><span>了</span><span>。</span><span>如果你的</span><span>linux</span><span>上没有</span><span>quota</span><span>，则需要你安装这个软件包</span> <span>quota-3.13-5.el5.RPM</span> <span>（其实版本是多少无所谓了，关键是这个软件包）</span><span>。quota</span><span>在实际应用中是针对整个分区进行限制的</span><span>。</span><span>如果你的</span><span>/dev/hda3</span> <span>是挂载在</span><span>/home</span> <span>目录下的，那么</span><span>/home</span> <span>所有目录都会受到限制</span><span>。</span>

<span>quota</span> <span>这个模块主要分为</span><span>quota quotacheck quotaoff quotaon quotastats edquota setquota warnquota repquota</span><span>这几个命令，下面就分别介绍这些命令</span><span>。</span>

<span>quota</span> <span>用来显示某个组或者某个使用者的限额</span><span>。</span>

<span>语法：</span><span>quota [-guvs] [user,group]</span>

<span>-g</span> <span>：显示某个组的限额</span>

<span>-u</span> <span>：显示某个用户的限额</span>

<span>-v</span> <span>：显示的意思</span>

<span>-s</span> <span>：选择</span><span>inod</span><span>或硬盘空间来显示</span>

<span> </span>

<span>quotacheck</span> <span>用来扫描某一个磁盘的</span><span>quota</span><span>空间</span><span>。</span>

<span>语法：</span><span>quotacheck [-auvg] /path</span>

<span>-a</span> <span>：扫描所有已经</span><span>mount</span><span>的具有</span><span>quota</span><span>支持的磁盘</span>

<span>-u</span> <span>：扫描某个使用者的文件以及目录</span>

<span>-g</span> <span>：扫描某个组的文件以及目录</span>

<span>-v</span> <span>：显示扫描过程</span>

<span>-m</span> <span>：强制进行扫描</span>

<span> </span>

<span>edquota</span> <span>用来编辑某个用户或者组的</span><span>quota</span><span>值</span><span>。</span>

<span>语法：</span><span>edquota [-u user] [-g group] [-t]</span>

<span>edquota -p user -u user</span>

<span>-u</span> <span>：编辑某个用户的</span><span>quota</span>

<span>-g</span> <span>：编辑某个组的</span><span>quota</span>

<span>-t</span> <span>：编辑宽限时间</span>

<span>-p</span> <span>：拷贝某个用户或组的</span><span>quta</span><span>到另一个用户或组</span>

<span>当运行</span><span>edquota -u user</span> <span>时，系统会打开一个文件，你会看到这个文件中有</span><span>7</span><span>列，它们分别代表的含义是：</span>

<span>Filesystem</span> <span>：磁盘分区，如</span><span>/dev/hda3</span>

<span>blocks</span> <span>：当前用户在当前的</span><span>Filesystem</span><span>中所占用的磁盘容量，单位是</span><span>Kb。</span><span>该值请不要修改</span><span>。</span>

<span>soft/hard</span> <span>：当前用户在该</span><span>Filesystem</span><span>内的</span><span>quota</span><span>值，</span><span>soft</span><span>指的是最低限额，可以超过这个值，但必须要在宽限时间内将磁盘容量降低到这个值以下</span><span>。hard</span><span>指的是最高限额，即不能超过这个值</span><span>。</span><span>当用户的磁盘使用量高于</span><span>soft</span><span>值时，系统会警告用户，提示其要在宽限时间内把使用空间降低到</span><span>soft</span><span>值之下</span><span>。</span>

<span>inodes</span> <span>：目前使用掉的</span><span>inode</span><span>的状态，不用修改</span><span>。</span>

<span>quotaon</span> <span>启动</span><span>quta</span><span>，在编辑好</span><span>quota</span><span>后，需要启动才能是</span><span>quta</span><span>生效</span>

<span>语法：</span><span>quotaon [-a] [-uvg directory]</span>

<span>-a</span> <span>：全部设定的</span><span>quota</span><span>启动</span>

<span>-u</span> <span>：启动某个用户的</span><span>quota</span>

<span>-g</span> <span>：启动某个组的</span><span>quota</span>

<span>-s</span> <span>：显示相关信息</span>

<span> </span>

<span>quotaoff</span> <span>关闭</span><span>quota</span>

<span>该命令常用只有一种情况</span> <span>quotaoff -a</span> <span>关闭全部的</span><span>quota</span>

<span>以上讲了很多</span><span>quota</span><span>的相关命令，那么接下来笔者教你如何在实践应用中去做这个磁盘配额</span><span>。</span><span>整个执行过程如下：</span>

<span>首先先确认一下，你的</span><span>/home</span><span>目录是不是单独的挂载在一个分区下，用</span><span>df</span> <span>查看即可</span><span>。</span><span>如果不是则需要你跟我一起做</span><span>。</span><span>否则这一步即可省略</span><span>。</span>

<span>![8_111.png.jpg](images/8_111.png.jpg)</span>

<span>笔者的</span><span>linux</span><span>系统中，</span><span>/home</span><span>并没有单独占用一个分区</span><span>。</span><span>所以需要把</span><span>/home</span><span>目录挂载在一个单独的分区下，因为</span><span>quota</span><span>是针对分区来限额的</span><span>。</span>

<span>![8_112.png.jpg](images/8_112.png.jpg)</span>

<span>笔者用</span><span>fdisk -l</span> <span>查看目前</span><span>/dev/hdb</span> <span>磁盘有</span><span>5</span><span>个可用分区，所以笔者打算把</span><span>/dev/hdb1</span><span>挂载在</span><span>/home</span> <span>目录下</span>

<span>![8_113.png.jpg](images/8_113.png.jpg)</span>

<span>看到了吧，目前笔者的</span><span>/home</span><span>目录已经是一个单独的分区了</span><span>。</span>

<span>1</span><span>）建立测试用户</span>

<span>![8_114.png.jpg](images/8_114.png.jpg)</span>

<span>首先建立一个</span><span>test</span><span>用户，则同时建立了一个</span><span>test</span><span>组</span><span>。</span><span>可以在</span><span>/etc/passwd</span><span>中有以</span><span>test</span><span>为开头的行，其中</span><span>uid</span><span>和</span><span>gid</span><span>都为</span><span>500</span> <span>，然后又建立一个</span><span>test1</span><span>账号，使其加入</span><span>test</span><span>组，查看</span><span>/etc/passwd</span><span>文件发现</span><span>test</span><span>和</span><span>test1</span><span>用户的</span><span>gid</span><span>都为</span><span>500。</span><span>（也许你对</span><span>/etc/passwd</span><span>文件</span><span>、</span><span>增加一个用户以及</span><span>uid</span><span>和</span><span>gid</span><span>等概念不熟悉，没有关系，在以后的章节中会做介绍，在这里只需要你明白即可）</span>

<span>2</span><span>）打开磁盘的</span><span>quota</span><span>功能</span>

<span>默认</span><span>linux</span><span>并没有对任何分区做</span><span>quota</span><span>的支持，所以需要我们手动打开磁盘的</span><span>quota</span><span>功能，你是否记得，在前面内容中分析</span><span>/etc/fstab</span><span>文件的第四列时讲过这个</span><span>quota</span><span>选项（</span><span>usrquota, grpquota</span><span>）</span><span>。</span><span>没错，要想打开这个磁盘的</span><span>quota</span><span>支持就是需要修改这个第四列的</span><span>。</span><span>用</span><span>vim</span><span>编辑</span><span>/etc/fstab</span> <span>加入一行，如下图：</span>

<span>![8_115.png.jpg](images/8_115.png.jpg)</span>

<span>vim</span><span>命令将会在后续章节详细介绍，前面介绍过如何进入编辑模式以及如何保存文件</span><span>。</span><span>如果你的</span><span>linux</span><span>系统已经有</span><span>/home</span><span>这一行，那么直接修改第四列，加上</span><span>usrquota,grpguota</span><span>（中间没有空格）</span><span>。</span><span>接下来需要重新挂载</span><span>/home。</span>

<span>![8_116.png.jpg](images/8_116.png.jpg)</span>

<span>另外你也可以这样实现重新挂载</span><span>/home</span>

<span>![8_117.png.jpg](images/8_117.png.jpg)</span>

<span>如何查看是否启用了</span><span>quota</span><span>呢？</span>

<span>![8_118.png.jpg](images/8_118.png.jpg)</span>

<span>只要查看</span><span>/etc/mtab</span><span>文件中</span><span>/home</span><span>所在那行是否有</span><span>usrguota,grpquota</span><span>即可</span><span>。</span><span>笔者的</span><span>/dev/hdb1</span><span>现在已经支持了</span><span>quota</span>

<span>3</span><span>）扫描磁盘的使用者使用状况，并产生重要的</span><span>aquota.group</span><span>与</span><span>aquota.user</span>

<span>这一步就需要用到</span><span>quotacheck</span><span>了，</span><span>aquota.group</span><span>与</span><span>aqouta.user</span><span>分别是组以及用户磁盘配额需要的配置文件</span><span>。</span><span>如果没有这两个文件，则磁盘配额是不会生效的</span><span>。</span>

<span>![8_119.png.jpg](images/8_119.png.jpg)</span>

<span>当首次使用</span><span>quotacheck</span><span>命令时，会提示</span><span>“cannot stat old user quota file ……”</span><span>其实这是在提示你在</span><span>/home</span><span>目录下没有</span><span>aquota.user</span><span>以及</span><span>aquota.group</span><span>两个文件</span><span>。</span><span>没有关系，因为以前并没有配置过磁盘配额，当然没有这两个文件了</span><span>。</span><span>当执行完</span><span>quotacheck</span><span>命令后，会在</span><span>/home</span><span>目录下生成这两个文件的</span><span>。</span>

<span>4</span><span>）启动</span><span>quota</span><span>配额</span>

<span>![8_120.png.jpg](images/8_120.png.jpg)</span>

<span>5</span><span>）编辑用户磁盘配额</span>

<span>先来设定</span><span>test</span><span>账户的配额，然后直接把</span><span>test</span><span>的配额拷贝给</span><span>test1</span><span>即可</span><span>。</span><span>这里就需要用到</span><span>edquota</span><span>了</span><span>。</span>

<span>![8_121.png.jpg](images/8_121.png.jpg)</span>

<span>讲上面内容修改为</span>

<span>![8_122.png.jpg](images/8_122.png.jpg)</span>

<span>其中单位是</span><span>Kb</span><span>，所以</span><span>soft</span> <span>值大约为</span><span>20Mb</span><span>，</span><span>hard</span><span>值为</span><span>30Mb</span><span>，保存这个文件，保存的方式跟</span><span>vim</span><span>一个文件的方式一样的</span><span>。</span>

<span>![8_123.png.jpg](images/8_123.png.jpg)</span>

<span>将</span><span>test</span><span>的配额复制给</span><span>test1。</span><span>下面继续设定宽限时间</span><span>。</span>

<span>![8_124.png.jpg](images/8_124.png.jpg)</span>

<span>默认是</span><span>7days</span> <span>在这里我们改为</span><span>1days。</span><span>下面查看一下</span><span>test</span><span>以及</span><span>test1</span><span>用户的配额吧</span><span>。</span>

<span>![8_125.png.jpg](images/8_125.png.jpg)</span>

<span>6</span><span>）编辑组磁盘配额</span>

<span>![8_126.png.jpg](images/8_126.png.jpg)</span>

<span>设定组</span><span>test</span><span>的</span><span>soft</span><span>配额值为</span><span>40M</span><span>，</span><span>hard</span><span>值为</span><span>50M。</span><span>下面查看组</span><span>test</span><span>的配额</span><span>。</span>

<span>![8_127.png.jpg](images/8_127.png.jpg)</span>

<span>7</span><span>）设定开机启动</span>

<span>前面已经讲到启动磁盘配额的命令是</span><span>quotaon -aug</span> <span>，所以要想开机启动，只需将这条命令加入到</span> <span>/etc/rc.d/rc.local</span><span>文件即可</span><span>。</span>

<span>![8_128.png.jpg](images/8_128.png.jpg)</span>

