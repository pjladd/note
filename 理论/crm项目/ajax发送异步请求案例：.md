# ajax发送异步请求案例：

![image-20230325070850329](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230325070850329.png)

```
$.ajax({
		url:'settings/qx/user/login.do',
		data:{
				loginAct:loginAct,
				loginPwd:loginPwd,
				isRemPwd:isRemPwd
		},
		type:'post',
		dataType:'json',
		success:function (data) {
				if(data.code=="1"){
					//跳转到业务主页面
					window.location.href="workbench/index.do";
				}else{
					//提示信息
					$("#msg").text(data.message);
				}
		},
		beforeSend:function () {
				//当ajax向后台发送请求之前，会自动执行本函数；
				//该函数的返回值能够决定ajax是否真正向后台发送请求：
				//如果该函数返回true,则ajax会真正向后台发送请求；否则，如果该函数返回false，则ajax放弃向后台发送请求。
					
					$("#msg").text("正在努力验证....");
					return true;
					
		}
});

```

