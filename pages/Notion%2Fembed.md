-
	- [[Notion/embed]] [[logseq/publish]]时出现问题
	  collapsed:: true
		- ~~我自己访问https://www.fpb.icu/# /grap都是白的？~~
		- 定位到问题了。
		- 成功在 [[logseq/publish]] 找到问题并提交 [[issues]]
			- 不可访问的，从Notion发出的agent
			- ```java
			  Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Notion/2.0.41 Chrome/102.0.5005.167 Electron/19.1.9 Safari/537.36
			  ```
			- 在浏览器中，用插件设定以上agent，访问logseq publish会出现白屏。
			- 把 `Electron/19.1.9` 删掉，成功访问。
			- ```java
			  Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Notion/2.0.41 Chrome/102.0.5005.167  Safari/537.36
			  ```
			- 发现问题，Logseq publish对含有`Electron/19.1.9`请求头的页面，响应会出现问题。
				- ```java
				  /* Wrap the content inside code blocks in all themes 
				  
				  pre, code {
				    white-space : pre-wrap !important;
				  }
				  
				  */
				  
				  ```
	- 尝试在 [[Notion]]里embed [[logseq]]这个发布页，但是不行。看了下响应头里面并没有 `x-frame-options: sameorigin`之类的东西。不清楚为啥，去提了个issues。#2023-03-31
	  collapsed:: true
		- 我以为
		  collapsed:: true
			- ~~我用vercle部署了Nobelium和logseq。Nobelium是可以embed进Notin，而logseq却不行。~~
			  ~~说明和部署平台无关~~
			- [nobelium blog](https://blog.fpb.icu)
			  [logseq blog ](https://fpb.icu)
			- [ignore -x-frame-chromium plus](https://chrome.google.com/webstore/detail/ignore-x-frame-headers/gleekbfjekiniecknbkamfmkohkpodhe)
			- 装完插件可以来[这里](https://blog.fpb.icu/embed-logseq-3W8e1nhGu9h9t6)看效果
			- 当用插件去除x-frame-options: sameorigin之类的东西时，logseq才可以在网页版notion中出现。
			  而我在指向logseq域名的请求中，并未看到x-frame-options: sameorigin之类的东西，所以不清楚发生了什么，故临此请教。
			  ![clipboard_20230401_000001](https://user-images.githubusercontent.com/128216091/229171418-aeab0725-cc7a-49f6-8df5-edf441dcc6a8.png)
		- [[Notion/embed]]
			- Notion客户端无法embed logseqweb
			- edge无插件Notion可以embedlogseqweb
			- 问题似乎不在logseqweb
			- 而在Notion客户端。可是Notion客户端除了目标网站禁止iframe才不显示外，难道自己也会有限制？
				- 自己的限制一种是云请求的黑名单限制，就是限制你不能embed，但实际上能embed的网址，比如p*b。
				  collapsed:: true
					- 但这种显示是可以通过二次跳转进入的。等于是逃过了notion的云检查。
						- 错了，Notion修复了二次跳转!p*b跳转不过去了。。
					- 有些网站又不需要跳转，就可以访问了。
					- 之前为什么需要跳转，是因为Notion对目标网站的解析有问题，所有跳转是解决Notion解析的问题。让他不要去解析。
					- 但现在，Notion可以解析了，那么跳转这一步就没必要了。
					- 然后，现在Notion把客户端里的iframe的跳转，和之前不同了。
			- 浏览器和手机中都可以emebed此网页。只有win客户端不行