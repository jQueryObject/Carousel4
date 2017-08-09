# jq淡入淡出全屏轮播效果Carousel4
效果如下：
![](images/img.gif)

all code:
```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>jq淡入淡出全屏轮播效果</title>
	<style>
		*{margin:0px;padding: 0px;}
		li{list-style: none;}
		a{text-decoration: none;}
		.block{display: block;}
		.none{display: none;}

		#bannerBg{width: 100%;height: 300px;}
		#bannerBg .banner{width: 760px;height: 300px;margin: 0 auto;overflow: hidden;position: relative;}
		#bannerBg .banner ul.pic_list{width: 20000%;}
		#bannerBg .banner ul li{float:left;}
		#bannerBg .banner ul.btn_list{padding:5px 10px;position: absolute;z-index: 9999;background: rgba(0,0,0,.5);border-radius:10px;left: 50%;bottom: 20px;margin-left: -42px;}
		#bannerBg .banner ul.btn_list li{width: 10px;height: 10px;border-radius:50%;border:1px solid #fff;margin-left: 5px;cursor: pointer;}
		#bannerBg .banner ul.btn_list li.checked{background: #fff;}
		#bannerBg .banner .banner_btn{position: absolute;background: url('images/button.png') no-repeat;width: 46px;height: 70px;display: block;z-index:99999;top:50%;margin-top:-35px;}
		#bannerBg .banner .next{right:0px;background-position: -48px -128px;display: none;}
		#bannerBg .banner .prev{background-position: 0px -128px;display: none;}
		#bannerBg .banner .prev:hover{background-position: -133px 5px;}
		#bannerBg .banner .next:hover{background-position: -181px 5px;}
		.bg4{background: #D6DBE1}
		.bg0{background: #2387D3}
		.bg1{background: #59AE47}
		.bg2{background: #161938}
		.bg3{background: #36A0D0}

	</style>
</head>
<body>
	<div id="bannerBg" class="bg0">
		<div class="banner">
			<ul class="pic_list">
				<li><a href="#"><img src="images/1.jpg" alt="" /></a></li>
				<li><a href="#"><img src="images/2.jpg" alt="" /></a></li>
				<li><a href="#"><img src="images/3.jpg" alt="" /></a></li>
				<li><a href="#"><img src="images/4.jpg" alt="" /></a></li>
				<li><a href="#"><img src="images/5.jpg" alt="" /></a></li>
			</ul>
			<ul class="btn_list">
				<li class="checked"></li>
				<li></li>
				<li></li>
				<li></li>
				<li></li>
			</ul>
			<a href="javascript:void(0)" class="next banner_btn"></a>
			<a href="javascript:void(0)" class="prev banner_btn"></a>
		</div>
	</div>
</body>
</html>
<script src="js/jquery-2.1.4.js"></script>
<script>
	window.onload = function(){
		var i = 0;
		var leng = $('ul.pic_list li').length;
		$('a.next').click(function(){
			clickNext();
		});
		$('a.prev').click(function(){
			i--;
			if(i<0){
				i=leng-1;
			}
			$('ul.pic_list li').stop().eq(i).fadeIn().siblings().stop().hide();
			$('ul.btn_list li').eq(i).addClass('checked').siblings().removeClass('checked');
			$('#bannerBg').addClass('bg'+i).removeClass('bg'+((i+1)>4?0:(i+1)));
		});
		$('.banner').hover(function(){
			set = clearInterval(set);
			$('.banner a.next,.banner a.prev').css('display','block');
		},function(){
			$('.banner a.next,.banner a.prev').css('display','none');
			set = setInterval(clickNext,2000)
		});
		$('ul.btn_list li').click(function(){
			i = $(this).index();
			$('ul.pic_list li').stop().eq(i).fadeIn().siblings().stop().hide();
			$(this).addClass('checked').siblings().removeClass('checked');
			$('#bannerBg').addClass('bg'+i).removeClass('bg'+((i+1)>4?0:(i+1)));
		});
		var set = setInterval(clickNext,2000);
		function clickNext(){
			i++;
			if(i>leng-1){
				i=0;
			}
			$('ul.pic_list li').eq(i).fadeIn(600).siblings().hide();
			$('ul.btn_list li').eq(i).addClass('checked').siblings().removeClass('checked');
			$('#bannerBg').addClass('bg'+i).removeClass('bg'+((i-1)<0?4:(i-1)));
		}
	}
</script>
```

