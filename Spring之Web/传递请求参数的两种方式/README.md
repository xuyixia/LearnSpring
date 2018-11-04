# 请求的两种方式

向服务端控制器（controller）传递信息的方式有两种，一种是“请求中带有查询参数”，另一种是“参数作为路径的一部分”。前者是较为普遍（传统）的用法，可以称之为“通过HTTP协议发起的RPC请求”，参数部分称之为“查询参数”，如`/user?id=12`；后者是后起之秀，可以称之为“面向资源（REST）请求”，参数部分称之为“路径参数/路径变量”，如`/user/12`。

前者要优于后者。（原因不大清楚）

[《百度百科——RPC》](https://baike.baidu.com/item/%E8%BF%9C%E7%A8%8B%E8%BF%87%E7%A8%8B%E8%B0%83%E7%94%A8%E5%8D%8F%E8%AE%AE/6893245?fromtitle=RPC&fromid=609861&fr=aladdin)  
[《RPC服务和HTTP服务对比》](https://blog.csdn.net/wangyunpeng0319/article/details/78651998)

目前对于什么是RPC只有个简单的了解，RPC远程过程调用，对于应用庞大且应用环境复杂的情况比HTTP效率要高。

## URL-Pattern
常见的URL-Pattern有：
1. /
2. /*
3. /*.do

它们有什么不同？  


## SpringMVC对两种请求方式的支持
对于“基于HTTP的RPC请求”，SpringMVC通过注解@RequestParam获取查询参数；对于“RESTful请求”，用注解@RequestMapping和@PathVariable来获取路径变量。

````java
 /**
  * 基于HTTP的RPC请求
 */
 @RequestMapping(method=RequestMethod.GET)
  public List<Spittle> spittles(
      @RequestParam(value="max", defaultValue=MAX_LONG_AS_STRING) long max,
      @RequestParam(value="count", defaultValue="20") int count) {
    return spittleRepository.findSpittles(max, count);
  }

 /**
  * RESTful请求
 */
  @RequestMapping(value="/{spittleId}", method=RequestMethod.GET)
  public String spittle(
      @PathVariable("spittleId") long spittleId, 
      Model model) {
    model.addAttribute(spittleRepository.findOne(spittleId));
    return "spittle";
  }

````


SPringMVC零注解 https://www.cnblogs.com/bfchuan/p/3820962.html


https://waylau.com/spring-mvc-use-jetty/

https://github.com/waylau/spring-5-book