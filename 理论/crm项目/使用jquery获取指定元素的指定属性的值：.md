# 使用jquery获取指定元素的指定属性的值：

  选择器.attr("属性名");//用来获取那些值不是true/false的属性的值.（因为attr()方法获取不到值为true/false的属性的值）
  选择器.prop("属性名");//用来获取值是true/false的属性的值.例如：checked,selected,readonly,disabled等。