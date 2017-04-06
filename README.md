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
	<script>
	$(function() {
$("#file_upload").change(function() {
var $file = $(this);
var fileObj = $file[0];
var windowURL = window.URL || window.webkitURL;
var dataURL;
var $img = $("#preview");
 
if(fileObj && fileObj.files && fileObj.files[0]){
dataURL = windowURL.createObjectURL(fileObj.files[0]);
$img.attr('src',dataURL);
}else{
dataURL = $file.val();
var imgObj = document.getElementById("preview");
// 两个坑:
// 1、在设置filter属性时，元素必须已经存在在DOM树中，动态创建的Node，也需要在设置属性前加入到DOM中，先设置属性在加入，无效；
// 2、src属性需要像下面的方式添加，上面的两种方式添加，无效；
imgObj.style.filter = "progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale)";
imgObj.filters.item("DXImageTransform.Microsoft.AlphaImageLoader").src = dataURL;
 
}
});
});</script>
<input id="file_upload" type="file" />
<div class="image_container">
<img id="preview" width="60" height="60">
</body>
</html>
