---
title: Sublime Text3 配置
author: JHPing
layout: post
---
<div>
	<p>sublime text3   <a href="https://www.sublimetext.com/3">Download</a></p>
	<div>


		<h3>安装配置</h3>
		<dl>
			<dt>1.Package Control组件安装。</dt>
			<dd>
				<pre><code>import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())</code></pre>
			</dd>
			<dt>2.下载完成之后重启Sublime Text 3。</dt>
			<dd><p></p></dd>
			<dt>3.如果在Perferences->中看到package control这一项，则安装成功。 </dt>
			<dd><p></p></dd>
			<dt>4.用Package Control安装插件的方法</dt>
			<dd>
				<p>
				按下Ctrl+Shift+P调出命令面板 
				输入install 调出 Install Package 选项并回车，然后在列表中选中要安装的插件。

				注意：安装插件时保持网络畅通，避免插件由于网络原因奔溃
				</p>
			</dd>	
		</dl>


		<h3>插件配置</h3>
		<dl>
			<dt>1.Emmet</dt>
			<dd><a href="https://scotch.io/tutorials/write-html-crazy-fast-with-emmet-an-interactive-guide">Emmet指南</a></dd>
			<dt>2.Alignment(代码对齐)</dt>
			<dd>使用方法：选中要调整的行，然后按 Ctrl+ Alt + A</dd>
			<dt>3.JsFormat</dt>
			<dd>JS格式化</dd>
			<dt>4.Colorsublime</dt>
			<dd>允许您在Sublime Text中立即更改当前的颜色方案</dd>
		</dl>

		<h3>主题配置</h3>
		<dl>
			<dt>1.Boxy</dt>
			<dd>自带多种主题风格，可以融合ihodevsublime-file-icons；切换主题风格不必改配置,个人推荐;</dd>
			<dt>2.Seti_UI</dt>
			<dd>非常好用的一款主题,个人推荐;</dd>
			<dt>3.Agila</dt>
			<dd>文件树中间距很大的文件夹，以便于阅读;</dd>
			<dt>4.Lanzhou</dt>
			<dd>边栏和编辑器之间的良好对比;</dd>
			<dt>5.itg:Flat</dt>
			<dd>一个扁平化设计风格主题,个人推荐</dd>
			<dt>6.Spacegray</dt>
			<dd>该主题在 UI 上没什么吸引人之处，但很适合编码;</dd>
			<dt>7.Solarized</dt>
			<dd>非常精确的颜色设置，这些颜色在不同的设备和不同的亮度环境下测试过;</dd>
			<dt>8.Predawn</dt>
			<dd>Predawn 非常漂亮，特别适合编写代码;</dd>
			<dt>9.Tron Legacy</dt>
			<dd>Tron 电影迷们可能会喜欢这一款主题，因为颜色相似;</dd>
			<dt>10.Tomorrow Theme</dt>
			<dd>Tomorrow 主题颜色丰富，有着强烈的对比,个人推荐;</dd>
			<dt>11.Brogrammar</dt>
			<dd>扁平而且性感的设计,个人推荐;</dd>
		</dl>
		<p>附上几款其他比较好的主题<a href="https://scotch.io/bar-talk/best-sublime-text-3-themes-of-2015-and-2016">best-sublime-text-3-themes</a></p>



		<h3>Less配置</h3>
		<dl>
			<dt>1.下载安装nodejs </dt>
			<dd><a href="https://nodejs.org/en/">node.js</a></dd>
			<dt>2.安装lessc。可用npm包管理器直接安装的</dt>
			<dd><pre><code>npm install less -g</code></pre></dd>
			<dt>3.检查lessc是不是安装成功</dt>
			<dd><pre><code>lessc -v</code></pre></dd>
			<dt>4.安装submile的less2css插件</dt>
			<dd>Package Control安装less2css， less（高亮）</dd>
			<dt>5.如果编译时submile报错</dt>
			<dd>
				在cmd里安装 less-plugin-clean-css插件
				<pre><code>npm install less-plugin-clean-css</code></pre>
			</dd>
		</dl>

		<h3>删除插件</h3>
		<dl>
			<dt>步骤</dt>
			<dd>
				如果想要删除插件，Ctrl+Shift+P调出命令面板，
				输入remove，调出Remove Package选项并回车，
				选择要删除的插件即可，当然，更新插件，upgrade packages，
				通过简单的几个命令就可以方便的管理我们的插件了
			</dd>
		</dl>
	</div>
</div>



