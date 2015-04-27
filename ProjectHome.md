<div>
<p>       <span>互联网的页面展现形式相当丰富，但是如果按页面结构特征来分类，却不外乎以下几种类型：首页（包括栏目首页），列表页，内容页，评论页。</span></p>
<p><span><span lang='EN-US'>(1) </span>首页</span><span lang='EN-US'>: </span>网站的首页<span lang='EN-US'>, </span>一般含有多个栏目、图片、动画<span lang='EN-US'>,</span>以及若干文章标题链接。如<span lang='EN-US'>: </span>网易首页。</p>
<p><span><span lang='EN-US'>(2) </span>列表页</span><span lang='EN-US'>: </span>信息以列表的方式给出<span lang='EN-US'>, </span>一般以表格的形式列出若干个条目<span lang='EN-US'>, </span>经常含有分页功能。例如<span lang='EN-US'>: </span>某论坛版面的文章标题列表。</p>
<p><span><span lang='EN-US'>(3) </span>内容页</span><span lang='EN-US'>: </span>指含有正文内容的底层网页<span lang='EN-US'>, </span>一般只含有不超过一篇的文章内容<span lang='EN-US'>, </span>无评论或评论较少。如<span lang='EN-US'>: </span>各类网站的含有具体某篇文章的底层网页。</p>
<p><span><span lang='EN-US'>(4) </span>评论页</span><span lang='EN-US'>: </span>除了含有正文<span lang='EN-US'>, </span>正文后面还跟有若干个评论<span lang='EN-US'>,</span>以论坛为代表。</p>
<p><span lang='EN-US'>       </span>在这几种类型之中，信息含量最大的当数内容页，它是我们平常摄取信息的主要来源。由于内容页的重要性，不同的<span lang='EN-US'>Web</span>站点为了加强内容页的展示，都会加入一些与内容相关或无关的信息块，如导航，广告等。虽然这些信息块在一定程度上有助于我们的延伸阅读，但很多情况下，我们只需要获取正文信息就可以了，其他信息块反倒成了一种干扰。如何从一个内容页面中，正确提取出正文信息，就成了一个研究课题。<span></span></p>
<p><span lang='EN-US'>       </span><span>在详述之前，先说一下正文提取的意义。以笔者的经历看来，应用包括但不限于以下几个方面。</span></p>
<p><span><span lang='EN-US'>(1) </span>采集，搜索。</span>信息采集很常见，互联网上超过<span lang='EN-US'>30%</span>的内容都是从其他<span lang='EN-US'>Web</span>站点采集而来。现在的采集系统或工具，大多是基于页面的正则来进行信息采集的，这样的优点是，对于需要采集的信息精确度很高，但是缺点也是很明显的，由于是基于页面的<span lang='EN-US'>Html</span>源码来采集，一旦源站点改版或调整，导致页面的<span lang='EN-US'>Html</span>源码改变，所有正则将全部作废。而正文提取技术，不是以<span lang='EN-US'>Html</span>源码格式为依据，所以<span lang='EN-US'>Html</span>源码的改变相对来说影响不大。</p>
<p><span><span lang='EN-US'>(2) </span>门户文章发布。</span>很多门户站点，并没有专门的记者团队，大部分文章都靠编辑在网上复制粘贴。如果能在发布界面加个功能，只需要输入网址，即可正确导入正文内容，并自动处理图片，想必是个不错的用户体验。</p>
<p><span><span lang='EN-US'>(3)Wap</span>浏览器。</span><span lang='EN-US'>Wap</span>浏览由于受到流量及手机屏幕的限制，现在的<span lang='EN-US'>Wap</span>页面大部分以特出文字信息为主，但也不排除会有一些干扰信息块出现。作为用户，希望能只显示正文信息，特别是对于新闻及小说等页面。<span lang='EN-US'>Wap</span>浏览器如果可以将正文内容自动提取出来，应该是个不错功能。<span lang='EN-US'>Android</span>系统的迷人浏览器有个阅读模式，算是在这方面的一个探索。</p>
<p><span lang='EN-US'><span> </span></span></p>
<p>       <span>正文提取技术的算法很多，本文是基于多特征的一种算法研究，根据信息块的特征进行判定。内容页又称为主题页，主题内容通常可以分解层次为<span lang='EN-US'>: </span>①标题<span lang='EN-US'>; </span>②发布时间<span lang='EN-US'>; </span>③内容正文<span lang='EN-US'>; </span>④相关文章或延伸性阅读。除了“内容正文”为必须元素外，其他几个元素都不一定会在内容页出现。根据对大量不同网页观察，各个元素的位置及表现形式虽无固定的标准，但是大部分却满足一定的特征。</span></p>
<p><span lang='EN-US'><span> </span></span></p>
<p>一．标题块</p>
<ul>
<li>分块节点：<span lang='EN-US'>td</span>，<span lang='EN-US'>div</span>，<span lang='EN-US'>h</span>，<span lang='EN-US'>span</span></li>
<li>一般位于<span lang='EN-US'>Head/Title</span>的位置</li>
<li>当前单元含有h1-h3，b，i，strong等标签</li>
<li>样式，一般<span lang='EN-US'>class</span>包含<span lang='EN-US'>title</span>，<span lang='EN-US'>head</span>等字符</li>
<li>文字长度，一般大于<span lang='EN-US'>3</span>个字符，小于<span lang='EN-US'>35</span>个字符</li>
</ul>
<p><span lang='EN-US'><span> </span></span></p>
<p>二．发表时间块</p>
<ul>
<li>分块节点：<span lang='EN-US'>td</span>，<span lang='EN-US'>div</span>，<span lang='EN-US'> span</span></li>
<li>文字长度，一般小于<span lang='EN-US'>50</span>个字符</li>
<li>包含日期格式（<span lang='EN-US'>2010-08-09</span>）的字符串</li>
<li>包含以下关键字：来源，发表</li>
</ul>
<p><span lang='EN-US'> </span></p>
<p>三．主题块</p>
<ul>
<li>分块节点：<span lang='EN-US'>td</span>，<span lang='EN-US'>div</span></li>
<li><span lang='EN-US'>HTML</span>网页中有一些特殊标签，通常只出现在网页主题块中，如<span lang='EN-US'>P,BR</span>等。因此，主题块中往往包含着特殊标签。</li>
<li>主题块内容含有较多的句子，因此具有较多逗号、句号等标点符号（<span lang='EN-US'>&gt;5</span>）。</li>
<li>若从信息量角度考虑，主题块一般是含有较多文字信息。</li>
<li>主题块的 标签密度=1000*标签数/文字数 应在小于一个范围。</li>
<li>主题块的 文本密度<span lang='EN-US'>=len(</span>文本<span lang='EN-US'>)/len(HTML</span>代码<span lang='EN-US'>) </span>较大</li>
<li>不应该包含 “上一篇”，“下一篇”</li>
<li>包含以下字符串的内容块，判定为包含版权信息，需减权：“<span lang='EN-US'>ICP</span>备<span lang='EN-US'>04000001</span>号”，“版权所有”，“<span lang='EN-US'>Copyright</span>”</li>
<li>主题块序号在标题块之下</li>
<li>主题块序号在发表时间块之下</li>
<li>主题块序号在相关链接块之上</li>
</ul>
<p><span lang='EN-US'><span> </span></span></p>
<p>四．相关链接块</p>
<ul>
<li>分块节点：<span lang='EN-US'>td</span>，<span lang='EN-US'>div</span></li>
<li>文字应为“相关链接”、“相关新闻”、“相关报道”等敏感词，且连接比例很高。</li>
<li>链接数小于<span lang='EN-US'>20</span></li>
</ul>
<p><span lang='EN-US'><span> </span></span></p>
<p>实现：<br />
根据以上信息块特征，采用特征提权算法，<span lang='EN-US'>C#</span>（<span lang='EN-US'>3.5</span>）编程实现，命名为<span lang='EN-US'>QD</span>正文提取组件。经测试，对<span lang='EN-US'>Html</span>格式规范的以文字为主的内容页，正确提取率在<span lang='EN-US'>85%</span>以上，各大门户的新闻页面在<span lang='EN-US'>95%</span>以上。</p>
<p><a href='http://www.qwolf.com/wp-content/uploads/2010/11/2010-11-11_132022.gif'><img src='http://www.qwolf.com/wp-content/uploads/2010/11/2010-11-11_132022-300x209.gif' alt='' height='209' width='300' title='2010-11-11_132022' /></a></p>
<p><span></span>更详细的内容请转至：<a href='http://www.qwolf.com/?p=791'>http://www.qwolf.com/?p=791</a></p>
<blockquote></div>