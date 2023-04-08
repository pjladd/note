# Handler方法的返回如果是转发的话，会存在将请求转发给另一个Controller的情况吗？

答：不存在，因为handler方法的返回如果是转发，SpringMVC会根据springmvc.xml上配置的，给handler方法返回的String的前面加上WEB-INF/...，后面加上后缀，如：.jsp。不可能是转发给一个Controller。

