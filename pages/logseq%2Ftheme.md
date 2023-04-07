-
	- [[logseq/theme]]
	  collapsed:: true
		- 主题1，地图背景
			- 在logseq/custom.css中插入下方代码，即可使用此主题
			- ```java
			  @import url('https://cdn.jsdelivr.net/gh/fishpigbird/logseq-clean-themes@main/bg.css');
			  ```
		- 主题2，点阵背景
			- ```java
			  /* 白黑主题   绿字， 点阵背景 */
			  @import url('https://piotrsss.github.io/logseq-tools/public/bujo-css/main.css');
			  @import url('https://piotrsss.github.io/logseq-tools/public/bujo-css/dark-black.css');
			  @import url('https://piotrsss.github.io/logseq-tools/public/bujo-css/dark-black-dots.css');
			  @import url('https://piotrsss.github.io/logseq-tools/public/bujo-css/light-white.css');
			  @import url('https://piotrsss.github.io/logseq-tools/public/bujo-css/light-white-dots.css');
			  
			  ```
		- 字体中宋
			- ```java
			   * {
			    font-family: STZhongsong, sans-serif;
			    font-size:19px;
			  }
			  ```
	- [[logseq/theme]] 将代码设置成wrap
	  collapsed:: true
		- ```java
		  /* Wrap the content inside code blocks in all themes 
		  
		  pre, code {
		    white-space : pre-wrap !important;
		  }
		  
		  */
		  
		  ```