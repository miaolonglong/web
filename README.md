	<!DOCTYPE html>
<html>
<head>
	<title></title>
	<meta charset="utf-8">
	<style>
		*{
			margin: 0px;
			padding: 0px;
		}
		ul,li{
			list-style: none;
		}
		#phead{
			width: 100%;
			height: 20px;
			background-color: #f7f7f7;
		}
		#title{
			width: 1200px;
			margin-right: 300px;
			margin:0 auto;
			overflow: hidden;
		}
		#text{
			margin-right: -100px;
		}
		#phead img{
			margin-left: 295px;
			float: left;
		}
		p{
	    	float: right;
	    	font-size: 12px;
	    	color: red;
	    }
	    #box{
	    	width: 1200px;
	    	height: 380px;
	    	margin-left:200px;
	    	margin-top: 10px;
	    	position: relative;
	    	overflow: hidden;
	    }
	    .box:hover #left{
	    	display: block;
	    }
	    .box:hover #right{
	    	display: block;
	    }
	    .slider{
	    	width: 8400px;
	    	position: absolute;
	    	left: -1200px;
	    }
	    .slide{
	    	width: 1200px;
	    	overflow: hidden;
	    	float: left;
	    }
	    .box>span{
	    	display: block;
	    	width: 30px;
	    	height: 50px;
	    	text-align: center;
	    	cursor: pointer;
	    	top: 175px;
	    	line-height: 50px;
	    	background:rgb(255,0,0);
	    	font-size: 30px;
	    	position: absolute;
	    	opacity: 0;
	    }
	    #left{
	    	position: absolute;
	    	left: 30px;
	    	bottom: 160px;
	    	width: 30px;
	    	height: 53px;
	    	background-color: red;
	    	text-align: center;
	    	font-size: 30px;
	    	color: white;
	    	opacity: 0.5;
	    	display: none;
	    }
	    #right{
	    	position: absolute;
	    	right: 30px;
	    	bottom: 160px;
	    	width: 30px;
	    	height: 53px;
	    	background-color: red;
	    	text-align: center;
	    	font-size: 30px;
	    	color: white;
	    	opacity: 0.5;
	    	display:none;
	    }
	    .nav{
	    	position: absolute;
	    	left: 500px;
	    	bottom: 10px;
	    }
	    .nav>li{
	    	float: left;
	    	width: 20px;
	    	height: 20px;
	    	background-color: #ccc;
	    	cursor: pointer;
	    	margin:0 10px;
	    	border-radius: 50%;
	    	text-align: center;
	    	font-size: 13px; 	
	    }
	    .nav .active{
	    	background:red;
	    }
    </style>
</head>
<body>
	<div id="phead">
		<img src="images/a15.png" id="pic">
		<div id="one">
		<div id="title">
			<p id="text">[温馨提示]最近有不少不法分子在网上骗人,请大家注意!!!</p>
		</div>
		</div>
	</div>
	<div id="box" class="box">
		<div class="slider" id="slider">
			<div class="slide"><img src="images/b5.png" alt=""></div>	 
		 	<div class="slide"><img src="images/b1.png" alt=""></div>
		 	<div class="slide"><img src="images/b2.png" alt=""></div>
			<div class="slide"><img src="images/b3.png" alt=""></div>
			<div class="slide"><img src="images/b4.png" alt=""></div>
			<div class="slide"><img src="images/b5.png" alt=""></div>	
			<div class="slide"><img src="images/b1.png" alt=""></div>	
		</div>
		<span id="left"><</span>
		<span id="right">></span>
		<ul class="nav" id="nav">
			<li class="active">1</li>
			<li>2</li>
			<li>3</li>
			<li>4</li>
			<li>5</li>
		</ul>
	</div>
</body>
<script type="text/javascript" src="js/animate.js"></script>
<script type="text/javascript">
	var wid = document.getElementById("title");
	var text = document.getElementById("text");
	var pic = document.getElementById("pic");
	setInterval(function() {
		if(parseInt(text.style.marginRight)>1200){
			text.style.marginRight=-10+"px";
		}
		else{
		 text.style.marginRight = (parseInt(text.style.marginRight)+1) + "px";
		}
    },30);
    animate(text,{"width":430,"marginLeft":0,"marginRight":-100});

	var box = document.getElementById('box');
	var oNavlist = document.getElementById('nav').children;
	var slider = document.getElementById("slider");
	var left = document.getElementById("left");
	var right = document.getElementById("right");
	var index = 1;
	var timer;
	var isMoving = false;

	for(var i=0;i<oNavlist.length;++i){
		oNavlist[i].index=i;
		oNavlist[i].onclick = function(){
			index = this.index+1;
			navmove();
			animate(slider,{left:-1200*index});
		}
	}
	function next(){
		if(isMoving){
			return;
		}
		isMoving=true;
		index++;
		navmove();
		animate(slider,{left:-1200*index},function(){
			if (index==6) {
				slider.style.left = "-1200px";
				index=1;
			}
			isMoving = false;
		});
	}
	function navmove(){
		for(var i =0;i<oNavlist.length;++i){
			oNavlist[i].className = "";
		}
		if(index>5){
			oNavlist[0].className = "active";
		}
		else if(index<=0){
			oNavlist[4].className = "active";
		}
		else{
			oNavlist[index-1].className="active";
		}
	}
	box.onmouseover = function(){
		animate(left,{opacity:50});
		animate(right,{opacity:50});
		clearInterval(timer);
	}
	box.onmouseout = function(){
		animate(left,{opacity:0});
		animate(right,{opacity:0});
		timer = setInterval(next,3000);
	}
	right.onclick = next;
	left.onclick = function(){
		if(isMoving){
			return;
		}
		isMoving =true;
		index--;
		navmove();
		animate(slider,{left:-1200*index},function(){
			if(index==0){
				slider.style.left="-6000px";
				index=5;
			}
			isMoving = false;
		})
	}
	timer = setInterval(next,3000);
</script>
</html>

<!-- 	function prev(){
		if(isMoving){
			return;
		}
		isMoving =true;
		index--;
		navmove();
		animate(slider,{left:-1200*index},function(){
			if(index==0){
				slider.style.left="-6000px";
				index=5;
			}
			isMoving = false;
		})
	} -->
