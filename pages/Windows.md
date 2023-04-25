-
- 1
	- 2
	-
	- #2023-04-24
		- 数据无价 #Windows
			- 进pe，为了能升级bios把efi向前扩容100mb。
			- 用disk天才删除一个小文件很多的文件夹，删着删着就蓝屏了。
			- 错误：
			  Stop Code: SYSTEM THREAD EXCEPTION NOT HANDLED
			  What failed: Ntfs.sys
			- 重启电脑，系统，pe进不去。
			  换内存条，进不去。
			  换另一个固态系统，进不去。
			- f2系统设置能进去。
			  f10 bios能进去去。
			- 把机械硬盘拔掉，可开机。
			- 机械竟然挂了？
			- [[2023-04-25]]
				- 去电脑城修，要170R。
				- 忘记砍价了，毕竟这加个应该可以买个新的了。
					- 但是吧，再便宜他也可能不愿挣这个钱了估计，毕竟也不挽留我。
		- [[Windows]] 关闭多次重启导致开机等待2小时，多次通过忘记密码跳过后，无法继续跳过，遂取消。
		  collapsed:: true
			- [由于失败的登录次数过多或重复关机，此登录选项已被禁用。请使用其他登录选项，或者保持设备开机至少2小时，然后重试。](https://blog.csdn.net/weixin_43590796/article/details/112093177)
			-
		- [[Windows]] C盘大文件
			- **hiberfil.sys**删除
				- `powercfg -h off` 关闭休眠并删除缓存
				- `powercfg -h on` 开启
				- 重启
					- 我是服了，再开启还是占用26G。
					- 不能移动，这么大也不好压缩。
			- pagefile.sys删除方法
				- 通常自己可以**在"我的电脑"右键"属性"→"高级"→"性能"→"高级"→"虚拟内存"中将所有盘的虚拟内存设置为无分页文件，并选择“设置”后重启系统**，就可以删除页面文件pagefile.sys。
			- Swapfile.sys文件
				- swapfile.sys 与pagefile.sys 文件的管理方式一致，**无法直接删除**。 由于采用了统一的管理方式，所以要禁用swapfile.sys 就得把虚拟内存给禁了，这样pagefile.sys 页面文件也就消失了。