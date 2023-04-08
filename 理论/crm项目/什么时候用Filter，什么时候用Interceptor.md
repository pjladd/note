# 什么时候用Filter，什么时候用Interceptor?



Filter和Interceptor都能拦截请求。

一般来讲，判断是应该用Filter还是Interceptor是看要实现的功能的复杂程度，简单的功能用Filter，复杂的功能用Interceptor。