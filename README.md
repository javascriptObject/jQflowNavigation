# jQuery楼梯导航

效果如下

![](images/img.gif)

全部代码如下：

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>楼梯是导航</title>
	<style>
		*{margin: 0px;padding: 0px;}
		li{list-style: none;}
		#header{text-align: center;width: 1200px;margin: 0 auto;}
		#main{width: 1200px;margin: 0 auto;}
		.louti{height:800px; text-align: center;margin-top:20px;font-size:30px;color: #000;font-family: Arial}
		#footer{text-align: center;width: 1200px;margin: 0 auto;}
		#fix_nav{position: fixed;z-index: 5;left: 34px;top:100px;display: none;}
		#fix_nav ul li{width: 30px;height: 30px;line-height: 30px;text-align: center;cursor: pointer;border-bottom: 1px dotted #999;position: relative;}
		#fix_nav ul li span{display: none;position: absolute;top: 0px;left: 0px;font-size: 12px;width: 30px;height: 30px;}
		#fix_nav ul li.hover span{display: block;background: #c81623;color: #fff; }/*鼠标移动上去的样式*/
		#fix_nav ul li.hover span.avtive{display: block;background: #c81623;color: #fff;}/*鼠标移动上去并且点击时的样式*/
		#fix_nav ul li span.avtive{color: #c81623;display: block;background-color: #fff;}/*鼠标点击时的样式*/
	</style>
</head>
<body>
	<div id="header">头部</div>
	<div id="main">
		<div class="louti" style="background:red;">服饰</div>
		<div class="louti" style="background:#fff;">美妆</div>
		<div class="louti" style="background:yellow;">手机</div>
		<div class="louti" style="background:red;">家电</div>
		<div class="louti" style="background:#c00;">数码</div>
		<div class="louti" style="background:red;">运动</div>
		<div class="louti" style="background:#000;">居家</div>
		<div class="louti" style="background:#abcdef;">母婴</div>
		<div class="louti" style="background:red;">食品</div>
		<div class="louti" style="background:#999;">图书</div>
		<div class="louti" style="background:#ff0;">服务</div>
		<div class="louti" style="background:#666;">楼层11</div>
	</div>
	<div id="footer">页尾</div>
	<div id="fix_nav">
		<ul>
			<li>1F<span>服饰</span></li>
			<li>2F<span>美妆</span></li>
			<li>3F<span>手机</span></li>
			<li>4F<span>家电</span></li>
			<li>5F<span>数码</span></li>
			<li>6F<span>运动</span></li>
			<li>7F<span>居家</span></li>
			<li>8F<span>母婴</span></li>
			<li>9F<span>食品</span></li>
			<li>10F<span>图书</span></li>
			<li class="last">11F<span>服务</span></li>
		</ul>
	</div>
</body>
</html>
<script type="text/javascript" src="js/jquery-2.1.js"></script>
<script>
	$(function(){
		//鼠标移动效果
		$('#fix_nav ul li').hover(function(){
			$(this).addClass('hover');
		},function(){
			$(this).removeClass('hover');
		});
		//鼠标点击效果
		var mark=1;
		$('#fix_nav ul li').click(function(){
			$(this).find('span').addClass('avtive');
			$(this).siblings().find('span').removeClass('avtive');
		});
		//点击导航跳转效果
		$('#fix_nav ul li').click(function(){
			mark = 2;
			var $index = $(this).index();
			var $divH = $('.louti').eq($index).offset().top;
			$('html,body').animate({scrollTop:$divH},500,function(){
				mark=1
			})
		});
		//获取浏览器滚动事件
		$(window).scroll(function(){
			var $top = $(this).scrollTop();//获取滚动条的高度
			if(mark==1){
				$('#main .louti').each(function(){
					$index = $(this).index();
					$H = $('#main .louti').eq($index).offset().top;
					if($top>=$H){
						$('#fix_nav li').eq($index).find('span').addClass('avtive');
						$('#fix_nav li').eq($index).siblings().find('span').removeClass('avtive')
					}
				});
			}
			//当滚动到一定高度时楼梯式导航消失与显示
			var $height = $(window).scrollTop();
			var $main_h = $('#main').offset().top;
			if($height>$main_h){
				$('#fix_nav').fadeIn(600);
			}else{
				$('#fix_nav').fadeOut(600);
			}
		})

	})
</script>
```

