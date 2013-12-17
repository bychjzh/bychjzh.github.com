---
layout: post
title: "python 命令行参数处理 getopt"
description: ""
category: "python"
tags: ["python"]
---
{% include JB/setup %}


#一、说明
	getopt是一个用于解析C语言风格命令行参数的Python模块。函数原型:getopt.getopt(args, options[, long_options])  

#二、代码示例

	import getopt, sys

	def main():
	    try:
		opts, args = getopt.getopt(sys.argv[1:], "ho:v", ["help", "output="])
	    except getopt.GetoptError as err:
		# print help information and exit:
		print str(err) # will print something like "option -a not recognized"
		usage()
		sys.exit(2)
	    output = None
	    verbose = False
	    for o, a in opts:
		if o == "-v":
		    verbose = True
		elif o in ("-h", "--help"):
		    usage()
		    sys.exit()
		elif o in ("-o", "--output"):
		    output = a
		else:
		    assert False, "unhandled option"
	    # ...

	if __name__ == "__main__":
	    main()

#三、处理Short Options
	getopt函数的第二个参数是短选项,如代码第5行中"ho:v",其中-h、-v表示不带参数的选项,-o表示带参数的选项,对于带参数的短选项需要在其后面跟上一个冒号 ":"

#四、处理Long Options
	getopt函数的第三个参数是长选项,其是一个数组,数组的每个元素表示一个长选项。如代码第5行中的["help","output="],其中--help表示不带参数的长选项,--output表示带参数的长选项,对于带参数的长选项需要在其后面跟上一个等号“=”
