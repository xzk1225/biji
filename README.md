# biji<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style>
		#box{width: 200px;height: 200px;border:1px solid red;}
	</style>
</head>
<body>
	<h3>讲拖拽的图片直接显示在div#box内</h3>
	<div id="box"> </div>
	<script>
	window.onload = function() {
		var  box=document.getElementById('box')
		box.ondragover = function() {
            return false;
        }




		box.ondrop=function(ent){
			var e=ent||event;
			var file=e.dataTransfer.files[0];

			var reader=new FileReader()
			 reader.readAsDataURL(file)
			reader.onload=function(){
				var img=document.createElement('img')
				img.src=this.result;
				img.width=200
				box.appendChild(img)
			}
			return false
		}
		
	}

	</script>
</body>
</html>
