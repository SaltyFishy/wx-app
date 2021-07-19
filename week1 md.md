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
