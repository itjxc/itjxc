- 👋 Hi, I’m @itjxc
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
itjxc/itjxc is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

 html:
   
  <canvas id="snow"></canvas>

  css
  * {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
#snow {
	width: 100%;
	height: 100vh;
	background: url("https://ts1.cn.mm.bing.net/th/id/R-C.251c4a3c281997690550ba45cd674fb0?rik=9Yl74uoJYzjYtQ&riu=http%3a%2f%2fseopic.699pic.com%2fphoto%2f40008%2f6731.jpg_wh1200.jpg&ehk=lfimizKlnOrF7N%2fpkaNIc0SY2Q0NYHUMMy12%2fE2%2bLOI%3d&risl=&pid=ImgRaw&r=0") no-repeat center / 100% 100%;
	display: block;
}

js
const canvas = document.querySelector("#snow")
const W = canvas.clientWidth
const H = canvas.clientHeight

// 设置canvas画布大小
canvas.setAttribute("width", W)
canvas.setAttribute("height", H)

const ctx = canvas.getContext("2d")


const config = {
	number: 200,  // 生成的雪花数量
	snowArr: [],
	pic: "https://www.deanhan.cn/wp-content/uploads/2017/12/snow.png"  // 雪花图片
}
let snowImg = new Image()
snowImg.src = config.pic

for (let i = 0; i < config.number; i++) {
	config.snowArr.push({
		x: Math.random() * W,  // 定义每片雪花的X轴
		y: Math.random() * H,  // Y轴
		toX: Math.random(),  // 雪花每一次渲染的X距离
		toY: Math.random() * 1 + 1,
		size: Math.random() * 20 + 5  // 雪花的大小
	})
}


const dropAnimation = () => {
	ctx.clearRect(0, 0, W, H)  // 清除画布重新渲染
	for (let i = 0; i < config.snowArr.length; i++) {
		let snow = config.snowArr[i]
		// ctx.beginPath()  绘制圆形雪花 后面直接图片代替
		// ctx.arc(snow.x, snow.y, snow.size, 0, Math.PI * 2, true)
		// ctx.fillStyle = "#666"
		// ctx.fill()
		ctx.drawImage(snowImg, snow.x, snow.y, snow.size, snow.size)

		snow.x = snow.x > W ? 0 : snow.x + snow.toX  // 每调一次函数向右移动一点
		snow.y = snow.y > H ? 0 : snow.y + snow.toY   // 向下移动
	}
	requestAnimationFrame(dropAnimation)
}
requestAnimationFrame(dropAnimation)
