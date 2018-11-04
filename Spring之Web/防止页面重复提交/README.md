# 防止页面重复提交

浏览器的哪些操作会导致重复提交请求呢？刷新和后退重新提交。  
哪些请求需要防止重复提交呢？POST请求。所以通常在POST请求过后重定向页面。  
考虑下如果请求的处理时间过长，此时刷新页面或后退重新提交的情况。  

https://blog.csdn.net/jasonssh/article/details/7528539

https://blog.csdn.net/kevindr/article/details/41249863