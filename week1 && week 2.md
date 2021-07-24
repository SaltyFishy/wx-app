<h1>wx小程序</h1>
由于项目需要，现在开始进行wx小程序的学习。<br/>
wx小程序开发与传统的web开发的对比
<table border="1">
	<tr>
	<td><strong>结构</strong></dt>
	<td><strong>web开发</strong></td>
	<td><strong>wx小程序开发</strong></td>
	</tr>
	<tr>
	<td>结构</dt>
	<td>html</td>
	<td>wxml</td>
	</tr>
	<tr>
	<td>样式</dt>
	<td>css</td>
	<td>wxss</td>
	</tr>
	<tr>
	<td>逻辑</dt>
	<td>javascript</td>
	<td>javascript</td>
	</tr>
	<tr>
	<td>配置</td>
	<td>无</td>
	<td>json</td>
	</tr>
</table>
由于视图层与逻辑层提供了数据传输与事件系统，开发者只需要关注数据、逻辑即可。<br>
基本的项目目录：
<img src="https://github.com/SaltyFishy/wx-app/blob/main/%E5%9F%BA%E6%9C%AC%E9%A1%B9%E7%9B%AE%E9%A1%B5%E9%9D%A2.jpg" alt="基本项目目录">
几个重要文件及其解释:
<ul>
	<li><strong>app.js</strong><br>
		小程序的入口文件，全局文件，不可缺少，也是小程序的核心文件，必须内置有App构造函数
	</li> 
	<li><strong>app.json</strong><br>
		当前小程序的全局配置，不可缺少，包括了小程序的所有页面路径、界面表现、网络超时时间、底部 tab 等。
	</li> 
	<li><strong>app.wxss</strong><br>
		全局样式，作用于全部界面。
	</li> 
	<li><strong>app.xwml</strong><br>
		类似web开发的html，但是在某些地方有所不同<br>
		<ul>
			<li>与html常用的div、p标签不同，wxml常用的标签有小view, button, text等</li>
			<li>多了一些 wx:if /wx:for这样的属性以及 {{ }} 这样的表达式,如：<img src="" alt="例">
			</li>
		</ul>
	</li> 
	<li><strong>project.config.json</strong><br>
		通常大家在使用一个工具的时候，都会针对各自喜好做一些个性化配置，例如界面颜色、编译配置等等，当你换了另外一台电脑重新安装工具的时候，你还要重新配置。<br>
		考虑到这点，小程序开发者工具在每个项目的根目录都会生成一个project.config.json，你在工具上做的任何配置都会写入到这个文件，当你重新安装工具或者换电脑工作时，你只要载入同一个项目的代码包，开发者工具就自动会帮你恢复到当时你开发项目时的个性化配置，其中会包括编辑器的颜色、代码上传时自动压缩等等一系列选项。（摘自微信开发者文档）
	</li> 
	<li><strong>sitemap.json</strong><br>
		用于配置小程序及其页面是否允许被微信索引
	</li> 
</ul>
<h2>app.json</h2>
app.json会默认在所有页面使用，除非在某个页面下使用了页面的json文件进行配置。<br>
QuickStart项目默认会生成一个app.json文件，内容有：
<code>

	{
  	 "pages":[
       "pages/index/index",
       "pages/logs/logs"
  	  ],
  	  "window":{
    	"backgroundTextStyle":"light",
    	"navigationBarBackgroundColor": "#fff",
    	"navigationBarTitleText": "Weixin",
    	"navigationBarTextStyle":"black"
  	  }
	}
</code>
其中pages写小程序包含了哪些页面，其中写在最前面的为进入小程序的第一个页面。<br>
window有很多项属性，具体属性的作用可在<a href="https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html#window" alt="window属性">window属性</a>查看。<br>
除了pages、window外，还有很多其他的属性，可参考<a href="https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html" alt="微信开发者文档">微信开发者文档app.json</a>查看。
<h2>page.json</h2>
区别于app.json，page.json是对具体的某个页面进行配置。<br>
但是页面配置只能配置app.json中window属性下的属性,并覆盖。
<h2>page.wxss</h2>
完全遵循css语法，但是却有一些独特的单位。
详情参考<a href="https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxss.html" alt="WXSS">WXSS</a>
<h2>模板语法</h2>
<h3>数据绑定</h3>
WXML中的动态数据均来自对应Page的data。
可参考
<a href="https://developers.weixin.qq.com/miniprogram/dev/reference/wxml/data.html" alyt="数据绑定">数据绑定</a><br>
注意：当绑定的数据类型为Boolean时，双引号（或单引号）与花括号之间不能有空格<br>
注意：当出现嵌套循环时，通过wx:for-item与wx:for-index重命名变量就很必要了。<br>
数据绑定实例：<img src="https://github.com/SaltyFishy/wx-app/blob/main/%E6%95%B0%E6%8D%AE%E7%BB%91%E5%AE%9Awxml.jpg" alt="数据绑定wxml">
<img src="https://github.com/SaltyFishy/wx-app/blob/main/%E6%95%B0%E6%8D%AE%E7%BB%91%E5%AE%9Ajs.jpg" alt="数据绑定js">
<img src="https://github.com/SaltyFishy/wx-app/blob/main/%E6%95%B0%E6%8D%AE%E7%BB%91%E5%AE%9A%E5%AE%9E%E4%BE%8B.jpg" alt="数据绑定实例">
可以发现这种语法也是支持运算的，在微信开发者文档中也有提及其支持的运算。
<h3>列表渲染</h3>
wx:for{{数组或对象}}重复渲染<br>
默认数组的当前项的下标变量名默认为index，数组当前项的变量名默认为item<br>
使用wx:for-item可以指定数组当前元素的变量名<br>
使用wx:for-index可以指定数组当前下标的变量名<br>
<img src="https://github.com/SaltyFishy/wx-app/blob/main/%E5%88%97%E8%A1%A8%E6%B8%B2%E6%9F%93wxml.png" alt="列表渲染wxml">
<img src="https://github.com/SaltyFishy/wx-app/blob/main/%E5%88%97%E8%A1%A8%E6%B8%B2%E6%9F%93js.jpg" alt="列表渲染js">
<img src="https://github.com/SaltyFishy/wx-app/blob/main/wxfor%E5%AE%9E%E4%BE%8B.jpg" alt="wxfor实例"><br>
除了wx:for以外，还有wx:key也是一种渲染列表的方式，具体作用在微信开发者文档中的描述似乎有点晦涩，我们直接看他给的实例：
<a href="https://developers.weixin.qq.com/s/tpg5tKmv6kZt" alt="实例">实例</a>
<img src="https://github.com/SaltyFishy/wx-app/blob/main/wxkey%E5%AE%9E%E4%BE%8B.jpg" alt="wxkey实例">
详情可参考<a href="https://developers.weixin.qq.com/miniprogram/dev/reference/wxml/list.html" alt="列表渲染">列表渲染</a>
<h3>条件渲染</h3>
wx:if="{{true/flase}}"<br>
<img src="https://github.com/SaltyFishy/wx-app/blob/main/%E6%9D%A1%E4%BB%B6%E6%B8%B2%E6%9F%93wxml%20.jpg" alt="条件渲染wxml">
<img src="https://github.com/SaltyFishy/wx-app/blob/main/%E6%9D%A1%E4%BB%B6%E6%B8%B2%E6%9F%93js.jpg" alt="条件渲染js">
<img src="https://github.com/SaltyFishy/wx-app/blob/main/wxif%E5%AE%9E%E4%BE%8B.jpg" alt="wxif实例">
除此之外还有使用属性hidden，这里暂不多做介绍。<br>
详情可参考<a href="https://developers.weixin.qq.com/miniprogram/dev/reference/wxml/conditional.html" alt="条件渲染">条件渲染</a>
<h3>template模板</h3>
WXML提供模板（template），可以在模板中定义代码片段，然后在不同的地方调用。<br>
这个功能其实没啥好说的，个人理解看成C++的类的设计就好了。。。。
<img src="https://github.com/SaltyFishy/wx-app/blob/main/%E6%A8%A1%E6%9D%BFwxml.jpg" alt="模板wxml">
<img src="https://github.com/SaltyFishy/wx-app/blob/main/%E6%A8%A1%E6%9D%BFjs.jpg" alt="模板js">
<img src="https://github.com/SaltyFishy/wx-app/blob/main/template%E5%AE%9E%E4%BE%8B.jpg" alt="template实例">
有需要时可参考<a href="https://developers.weixin.qq.com/miniprogram/dev/reference/wxml/template.html" alt="template模板">template模板</a>
<h3>框架</h3>





<h3></h3>
