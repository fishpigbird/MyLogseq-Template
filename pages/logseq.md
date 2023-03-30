-
	- 尝试用.ignore来解决 [[logseq]]  自动 [[git]] 同步对非git库操作而导致的错误提醒
	  collapsed:: true
		- ![image.png](../assets/image_1680187421524_0.png)
			- 很好，对于仓库中已经存在着的文件的更改是可以更新的。
			  但是其他所有文件就全部无视掉了。
				- ![image.png](../assets/image_1680188243297_0.png)
					- 所以，我们复制3个文件.git readme.me .gitignore到其他我们不想被提醒git失败的非git仓库中即可。