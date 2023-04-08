# jquery事件函数的用法：



   选择器.click(function(){//给指定的元素添加事件
      //js代码
   });

   选择器.click();//在指定的元素上模拟发生一次事件



示例：

```
<script type="text/javascript">
	$(function () {
		//给整个浏览器窗口添加键盘按下事件
		$(window).keydown(function (e) {
			//如果按的是回车键，则提交登录请求
			if(e.keyCode==13){
				$("#loginBtn").click();  //由于下面的代码中已经为$("#loginBtn")添加事件了，所以执行本行代码时，就会发生下面的代码中给$("#loginBtn")添加的事件。
			}
		});

		//给"登录"按钮添加单击事件
		$("#loginBtn").click(function () {
			//收集参数
			var loginAct=$.trim($("#loginAct").val());
			var loginPwd=$.trim($("#loginPwd").val());
			var isRemPwd=$("#isRemPwd").prop("checked");
			//表单验证
			if(loginAct==""){
				alert("用户名不能为空");
				return;
			}
			if(loginPwd==""){
				alert("密码不能为空");
				return;
			}

			//显示正在验证
			//$("#msg").text("正在努力验证....");
			//发送请求
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
				beforeSend:function () {//当ajax向后台发送请求之前，会自动执行本函数；
					                    //该函数的返回值能够决定ajax是否真正向后台发送请求：
									    //如果该函数返回true,则ajax会真正向后台发送请求；否则，如果该函数返回false，则ajax放弃向后台发送请求。
					$("#msg").text("正在努力验证....");
					return true;
				}
			});
		});
	});
</script>
```

