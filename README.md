Rhomobile 中文文档
==================

注：本中文不忠于原文，仅供个人理解使用

如果您想参与，fork一下，提交给我

这个工具是基于超牛B的heroku-docs(https://github.com/heroku/heroku-docs)项目的

安装
-----
* Windows上? [安装](https://github.com/oneclick/rubyinstaller/wiki/Development-Kit) 这个 [Development Kit](http://rubyinstaller.org/downloads/). 然后再运行:

		$ gem install rdiscount --platform=ruby -v=1.6.8

* 然后再:

		# install prereqs and shotgun the docs server
		$ cd rhomobile-docs
		$ sudo gem install bundler (if you don't have it already)
		$ bundle install
		$ rake start #=> this will start the server and load the docs home page in your browser
	
重构 & 发行
-----------------------
这个程序将载入在config.yml中指定的子目录的内容

上传到heroku（前提是你已经有heroku账号）
	$ git add docs/
	$ git commit -m "adding new docs"
	$ git push heroku master

**注意: 不要 checkin 到docs/(子目录) (如docs/rhodes/).  docs/(子目录) 在其它的库中维护.  如,  docs/rhodes/ 在库 rhodes repo [https://github.com/rhomobile/rhodes](https://github.com/rhomobile/rhodes)中.**

About
----
weiz翻译部分内容

Originally written by Ryan Tomayko and Adam Wiggins.  This application is maintained by Rhomobile Dev.

Code is released under the [MIT License](http://www.opensource.org/licenses/mit-license.php)

All rights reserved on the content (text files in the docs subdirectory), although you're welcome to modify these for the purpose of suggesting edits.