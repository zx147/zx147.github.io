<!doctype html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Forever Love</title>
<link type="text/css" rel="stylesheet" href="css/default.css">
<script type="text/javascript" src="js/jquery.min.js"></script>
<script type="text/javascript" src="js/jscex.min.js"></script>
<script type="text/javascript" src="js/jscex-parser.js"></script>
<script type="text/javascript" src="js/jscex-jit.js"></script>
<script type="text/javascript" src="js/jscex-builderbase.min.js"></script>
<script type="text/javascript" src="js/jscex-async.min.js"></script>
<script type="text/javascript" src="js/jscex-async-powerpack.min.js"></script>
<script type="text/javascript" src="js/functions.js" charset="utf-8"></script>
<script type="text/javascript" src="js/love.js" charset="utf-8"></script>
<style type="text/css">
<!--
.STYLE1 {
	color: #666666
}
-->
</style>
</head>
<body>

<div id="main">
  <div id="error">本页面采用HTML5编辑，目前您的浏览器无法显示，请换成谷歌(<a href="http://www.google.cn/chrome/intl/zh-CN/landing_chrome.html?hl=zh-CN&brand=CHMI">Chrome</a>)或者火狐(<a href="http://firefox.com.cn/download/">Firefox</a>)浏览器，或者其他游览器的最新版本。</div>
  <div id="wrap">
    <div id="text">
      <div id="code"> 
      	<font color="#FF0000">
            <!--鱼油修改此处即可-->
            <span class="say">我爱你，不光因为你的样子，</span><br>
            <span class="say">还因为，和你在一起时，我的样子。</span><br>
            <span class="say">我爱你，不光因为你为我而做的事，</span><br>
            <span class="say">还因为，为了你，我能做成的事。</span><br>
            <span class="say"> </span><br>
            <span class="say">我爱你，因为你能唤出，</span><br>
            <span class="say">我最真的那部分。</span><br>
            <span class="say">我爱你，因为你穿越我心灵的旷野，</span><br>
            <span class="say">如同阳光穿透水晶般容易，</span><br>
            <span class="say"> </span><br>
            <span class="say">我的傻气，我的弱点，</span><br>
            <span class="say">在你的目光里几乎不存在。</span><br>
            <span class="say">而我心里最美丽的地方，</span><br>
            <span class="say">却被你的光芒照得通亮。</span><br>

            
            <span class="say"> </span><br>
            <span class="say"><span class="space"></span> -- 罗伊·克里夫特《爱》</span><br><br><br>

            <font color="yello"><span class="say" ><b>   --来自爱你的张鑫</b></span></font>
        </font>
        </p>
      </div>
    </div>
    <div id="clock-box"> <span class="STYLE1"></span><font color="#33CC00">亲爱的柔西，我爱你</font> <span class="STYLE1">已经是……</span>
      <div id="clock"></div>
    </div>
    <canvas id="canvas" width="1100" height="680"></canvas>
  </div>
</div>
<script>
    </script>
<script>
    (function(){
        var canvas = $('#canvas');
		
        if (!canvas[0].getContext) {
            $("#error").show();
            return false;        }

        var width = canvas.width();
        var height = canvas.height();        
        canvas.attr("width", width);
        canvas.attr("height", height);
        var opts = {
            seed: {
                x: width / 2 - 20,
                color: "rgb(190, 26, 37)",
                scale: 2
            },
            branch: [
                [535, 680, 570, 250, 500, 200, 30, 100, [
                    [540, 500, 455, 417, 340, 400, 13, 100, [
                        [450, 435, 434, 430, 394, 395, 2, 40]
                    ]],
                    [550, 445, 600, 356, 680, 345, 12, 100, [
                        [578, 400, 648, 409, 661, 426, 3, 80]
                    ]],
                    [539, 281, 537, 248, 534, 217, 3, 40],
                    [546, 397, 413, 247, 328, 244, 9, 80, [
                        [427, 286, 383, 253, 371, 205, 2, 40],
                        [498, 345, 435, 315, 395, 330, 4, 60]
                    ]],
                    [546, 357, 608, 252, 678, 221, 6, 100, [
                        [590, 293, 646, 277, 648, 271, 2, 80]
                    ]]
                ]] 
            ],
            bloom: {
                num: 700,
                width: 1080,
                height: 650,
            },
            footer: {
                width: 1200,
                height: 5,
                speed: 10,
            }
        }

        var tree = new Tree(canvas[0], width, height, opts);
        var seed = tree.seed;
        var foot = tree.footer;
        var hold = 1;

        canvas.click(function(e) {
            var offset = canvas.offset(), x, y;
            x = e.pageX - offset.left;
            y = e.pageY - offset.top;
            if (seed.hover(x, y)) {
                hold = 0; 
                canvas.unbind("click");
                canvas.unbind("mousemove");
                canvas.removeClass('hand');
            }
        }).mousemove(function(e){
            var offset = canvas.offset(), x, y;
            x = e.pageX - offset.left;
            y = e.pageY - offset.top;
            canvas.toggleClass('hand', seed.hover(x, y));
        });

        var seedAnimate = eval(Jscex.compile("async", function () {
            seed.draw();
            while (hold) {
                $await(Jscex.Async.sleep(10));
            }
            while (seed.canScale()) {
                seed.scale(0.95);
                $await(Jscex.Async.sleep(10));
            }
            while (seed.canMove()) {
                seed.move(0, 2);
                foot.draw();
                $await(Jscex.Async.sleep(10));
            }
        }));

        var growAnimate = eval(Jscex.compile("async", function () {
            do {
    	        tree.grow();
                $await(Jscex.Async.sleep(10));
            } while (tree.canGrow());
        }));

        var flowAnimate = eval(Jscex.compile("async", function () {
            do {
    	        tree.flower(2);
                $await(Jscex.Async.sleep(10));
            } while (tree.canFlower());
        }));

        var moveAnimate = eval(Jscex.compile("async", function () {
            tree.snapshot("p1", 240, 0, 610, 680);
            while (tree.move("p1", 500, 0)) {
                foot.draw();
                $await(Jscex.Async.sleep(10));
            }
            foot.draw();
            tree.snapshot("p2", 500, 0, 610, 680);
            
            canvas.parent().css("background", "url(" + tree.toDataURL('image/png') + ")");
            canvas.css("background", "#ffe");
            $await(Jscex.Async.sleep(300));
            canvas.css("background", "none");
        }));

        var jumpAnimate = eval(Jscex.compile("async", function () {
            var ctx = tree.ctx;
            while (true) {
                tree.ctx.clearRect(0, 0, width, height);
                tree.jump();
                foot.draw();
                $await(Jscex.Async.sleep(25));
            }
        }));

        var textAnimate = eval(Jscex.compile("async", function () {
		    var together = new Date();
		    together.setFullYear(2020,6,1); 			//时间年月日
		    together.setHours(16);						//小时	
		    together.setMinutes(53);					//分钟
		    together.setSeconds(0);					//秒前一位
		    together.setMilliseconds(2);				//秒第二位

		    $("#code").show().typewriter();
            $("#clock-box").fadeIn(500);
            while (true) {
                timeElapse(together);
                $await(Jscex.Async.sleep(1000));
            }
        }));

        var runAsync = eval(Jscex.compile("async", function () {
            $await(seedAnimate());
            $await(growAnimate());
            $await(flowAnimate());
            $await(moveAnimate());

            textAnimate().start();

            $await(jumpAnimate());
        }));

        runAsync().start();
    })();
    </script>





</body>
</html>
