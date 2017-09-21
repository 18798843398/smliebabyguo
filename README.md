<!DOCTYPE html>
<html>

	<head>
		<meta charset="utf-8">
		<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
		<title>轮播练习</title>
		<meta name="description" content="">
		<meta name="keywords" content="">
		<link href="" rel="stylesheet">
		<style>
			* {
				padding: 0;
				margin: 0;
				list-style: none;
			}
			
			.msg-banner {
				margin: 100px auto;
				width: 300px;
				height: 30px;
				position: relative;
				overflow: hidden;
			}
			
			.msg-banner-warp {
				width: auto;
				height: auto;
				position: absolute;
				top: 0;
				left: 0;
			}
			
			.msg-banner-warp li {
				height: 30px;
				line-height: 30px;
				text-align: right;
			}
		</style>
	</head>

	<body>
		<div class="msg-banner">
			<ul class="msg-banner-warp">
			</ul>
		</div>
		<script type="text/javascript" src="js/jquery-1.11.0.js"></script>
		<script>
			$(function() {
				function doPrint() {
					var html = "";
					for(var i = 0; i < 10; i++) {
						html += "<li><a href=\"javascript:;\">打印消息" + i + "</a></li>"
					}

					$(".msg-banner-warp").html(html);

					//打印消息的轮播
					var bannerIndex = 0;
					console.log(bannerIndex);
					var clone = $(".msg-banner .msg-banner-warp li").first().clone();
					$(".msg-banner .msg-banner-warp").append(clone);
					var bannerSize = $(".msg-banner .msg-banner-warp li").size();
					clearInterval(t);
					/*自动轮播*/
					if(bannerSize > 1) {
						var t = setInterval(function() {
							bannerIndex++;
							move();
							//console.log(bannerIndex);
						}, 2000);
					}

					function move() {
						if(bannerSize > 1) {
							if(bannerIndex == bannerSize) {
								$(".msg-banner .msg-banner-warp").css({ top: 0 });
								bannerIndex = 1;
							}
							if(bannerIndex == -1) {
								$(".msg-banner .msg-banner-warp").css({ top: -(bannerSize - 1) * 30 });
								bannerIndex = bannerSize - 2;
							}
							$(".msg-banner .msg-banner-warp").stop().animate({ top: -bannerIndex * 30 }, 500);
						}
					}

					//对banner定时器的操作
					$(".msg-banner").hover(function() {
						clearInterval(t);
					}, function() {
						t = setInterval(function() {
							bannerIndex++;
							move();
						}, 2000);
					});
				}

				doPrint();
				printTimerss11 = setInterval(doPrint, 10000);

				$(".msg-banner").on("click", "a", function() {
					alert($(this).text());
				});
			});
		</script>
	</body>

</html>
