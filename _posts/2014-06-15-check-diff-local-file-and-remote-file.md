---
layout: post
title: "check diff local file and remote file"
description: ""
category: 
tags: []
---
{% include JB/setup %}
总觉得rsync同步的时候丢了文件，所有用shell写个小脚本检测一下远程目录和本地目录的文件差异，代码如下：

```PowerShell
path="$1"
echo $1
if [ $# -lt 1 ];then
    echo "参数不完整"
    exit 0
fi

filename=`ssh 用户名@你的ip ls -R ${path}`
for name in $filename
do
    file=`echo ${name} | grep /`
    if [ -z "${file}" ];then  
        #echo "${path}${name}"
        if [ ! -e "${path}${name}" ];then
            echo "${path}${name} 0"
        fi
    else
        path="${name%:*}/"
        #echo "${path}----------------------------"
fi
done
```
*如果文件名称中有空格会认为是两个文件，算是个未解决的问题*
