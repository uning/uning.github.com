---
layout: post
title: "新浪微博侧栏widget定制-Octress"
date: 2011-11-05 13:11
comments: true
categories: 
- Tech
- Blog
- weibo
- 微博
---
Octresss毕竟是国外的人做的，国内服务几乎没加
不过，参照twitter，添加新浪微博侧栏也就是几分钟的事情
 
 定制侧栏的文件放在 source/\_includes/asides/下
1. 创建文件weibo.html
``` html source/\_includes/asides/weibo.html
{% if site.weibo_user %}
<section>
 <p>
<a  id="hover_pop" href="http://weibo.com/{{site.weibo_user}}"  wb_user_id="{{site.weibo_userid}}" >{{site.weibo_user}}@Weibo<span id="wb_follow_btn"> </a>
	</p>
  <script src="http://tjs.sjs.sinajs.cn/open/api/js/wb.js?appkey=1166443256" type="text/javascript"> </script>
  <script type="text/javascript">
	WB2.anyWhere(function(W){
		W.widget.hoverCard({
			id: "hover_pop"
			});


		W.widget.followButton({
		//uid: '{{ site.weibo_userid}}',
		uid: '{{site.weibo_userid}}',
		id: "wb_follow_btn"
        });
      });

  </script>
</section>
{% endif %}
```
2. 在_config.yml，添加,当然将 weibo_xxx改成你的就ok了
``` yml 
#Sina weibo
weibo_user: tingkunz
weibo_userid: 1769520197
```
搞定!

