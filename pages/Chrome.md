-
- 地址栏复制后，在logseq粘贴没有标题。而edge是有的 #TODO
-
- [[Chrome]]插件
  id:: 645a4646-2d11-4a45-b90d-b2f6f08df5e5
	- 导出插件
	  collapsed:: true
		- 用everything搜插件-关于内的包名，如 `goutbwnjrpsjtgnioudiyuebtrrynsr`
	- [划词翻译 - Chrome 应用商店 (google.com)](https://chrome.google.com/webstore/detail/%E5%88%92%E8%AF%8D%E7%BF%BB%E8%AF%91/ikhdkkncnoglghljlkmcimlnlhkeamad)
	  collapsed:: true
		- 介绍
			- 网页全文翻译需要VIP，用着谷歌和DeepL的免费api来盈利，我是不会付费的。（确实付过费。。）
		- v9.2.2 / [[DeepL]] 全网页翻译已失效
			- 217.js
				- ```java
				  pageTranslateLimit
				  videoLimit
				  ```
		- v9.8.0 / [[DeepL]] 可以
			- 63.js
				- ```java
				  const ut=114514,pt=new ke.P("pageTranslateLimit",ut)
				  ```
		- v10.1.0
			- 214.js
				- ```java
				  const mt=114514,gt=new ke.P("pageTranslateLimit",mt)
				  ```
	- [沉浸式翻译 - Chrome 应用商店 (google.com)](https://chrome.google.com/webstore/detail/immersive-translate/bpoadfkcbjbfhfodiogcnhhhpibjhbnh/related?hl=zh-CN)
	  collapsed:: true
		- 介绍
			- 这个也挺好用，翻译完的内容可以被[[简悦]]直接捕获，但不能切换全中文或全英文显示，只能双语同显示。开源，免费。
			- 这个插件和上面那个很像，~~我曾经记得可能在沉浸翻译里打开过划词翻译的介绍页面，感觉他俩多少有点关系？~~
	- [Link Map - Chrome 应用商店 (google.com)](https://chrome.google.com/webstore/detail/link-map/jappgmhllahigjolfpgbjdfhciabdnde)
		- 1.1.4
			- TAB GROUP
				- ```java
				  
				  import.js
				  isProUser:!1
				  改成isProUser:!0
				    
				    
				  tree.js 同上
				  好像一直是0
				  
				  
				  ```
			- side bar
				- tree.js
				- ```java
				  disabled: !wi(o)
				    
				    sName:"settings-select-popup",disabled:!wi(o),options:a})
				  改成disabled:false
				  ```
	-