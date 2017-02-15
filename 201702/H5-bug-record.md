>现象描述： 周一早上，来发现钱咖引流页未下载咖购应用时，跳转的中间页（mlink-middle.html）渲染成了源代码，LF同志查看得知
Response Heaers的Content-Type: application/octet-stream（二进制流，不知道下载文件类型，据说因为nginx无法识别文件类型，而返回的默认类型）

解决思路： 查看mini-site/public 下的软链，发现旧软链的添加方法是：ln -s ../mlink-middle-page/mlink-middle.html mlink-middle
使用是的链接： http://sns.kagou.me/mlink-middle?xx=xx   
这里mlink-middle可能被nginx解析为文件夹，而不是html文件， 导致返回类型错误；

解决方法： 重新设置软连接为 ln -s ../mlink-middle-page/mlink-middle.html mlink-middle.html  即，给新的软链名加上.html后缀。
注：周四晚上，又发现该页面报错，表现为页面内容显示是软连接，经查看是 后上的分支因为合并别人分支的时候，不小心把重设的软链覆盖了，导致软链失效。人为失误导致。
 * 合别人代码是要仔细检查每一处更改
 * 查看软链命令：public> ls -htl


