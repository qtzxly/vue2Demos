<template>
  <div class="about">
    <h1>This is an about page</h1>
    <video ref="video1" src="https://media.w3.org/2010/05/sintel/trailer.mp4" type="video/mp4"></video>

    <video controls ref="video">
      <source src="https://media.w3.org/2010/05/sintel/trailer.mp4" type="video/mp4">
    </video>
		<button @click="clickButton1">1111</button>
  </div>
</template>

<script>
	export default {
		data() {
			return {
			}
		},
		methods: {
			clickButton1() {
				console.log(111, this.$refs.video);
				// var player = document.getElementById("player01"); //获取video的Dom节点
				var player = this.$refs.video; //获取video的Dom节点
				player.setAttribute("crossOrigin", "anonymous"); //添加srossOrigin属性，解决跨域问题
				var canvas = document.createElement("canvas");

				canvas.width = player.clientWidth;
				canvas.height = player.clientHeight;
				// canvas = canvas.getContext("2d")
				canvas.getContext("2d").drawImage(player.childNodes[0], 0, 0, canvas.width, canvas.height); //截
				var dataURL = canvas.toDataURL("image/png"); //将图片转成base64格式
				let str = ` <li class="screenshot-item">
				    <div class="shot-time">2022-10-17</div>
				    <img src="${dataURL}" alt="" class="shot-img">
				</li>`
				$("#screenshot-list").append(str); //显示在页面中
				viewer.destroy(); //需要先销毁再渲染
				viewer = new Viewer(document.getElementById(`screenshot-list`))
			}
		}
	}
</script>

