<template>
	<div class="hello">
		<h1>{{ msg }}</h1>
		<p>{{ count }}</p>
		<button v-on:click="changeCount()">+</button>
		<!-- 插值表达式不能应用在设置属性上 -->
		<ul v-html="li"></ul>
		<div>
			<div>{{danger}}</div>
			<input type="radio" name="sex" :checked="danger===1" v-on:click="danger=1">男
			<input type="radio" name="sex" :checked="danger===0" v-on:click="danger=0">女
		</div>
		<div>
			<div v-if="danger===1">♂男</div>
			<div v-if="danger===0">♀女</div>
		</div>
		<!-- 考试成绩评定 -->
		<div>考试成绩为:{{cj}}</div>
		<!-- <div>
			<span></span>
			<span></span>
			<span></span>
			<span></span>
		</div> -->
		<!-- for循环 -->
		<div>
			<span v-for="(str,i) in pf" :key="i">{{str}}</span>
		</div>
		<h2>点击按钮换图</h2>
		<h2>
			<button @click="changeImg('-')">上一张</button>
			<span>{{ rotation[rotationIndex].name }}</span>
			<button @click="changeImg('+')">下一张</button>
		</h2>
		<div v-show="isAlert">图片到头了!!!!</div>
	</div>
</template>

<script>
	export default {
		name: "HelloWorld",
		data() {
			return {
				count: 0,
				msg: "hello Vue",
				li: "<li>这是一个li标签</li>",
				danger: 1,
				cj: 76.5,
				rotationIndex: 0,
				isAlert: false,
				pf: [
					"成绩评定A,....",
					"成绩评定B,....",
					"成绩评定C,....",
					"成绩评定D,....",
				],
				rotation: [{
						id: 1,
						"name": "波仔1",
						"img": "1.jpg"
					},
					{
						id: 2,
						"name": "波仔2",
						"img": "2.jpg"
					},
					{
						id: 3,
						"name": "波仔3",
						"img": "3.jpg"
					},
					{
						id: 4,
						"name": "波仔4",
						"img": "4.jpg"
					},
					{
						id: 5,
						"name": "波仔5",
						"img": "5.jpg"
					},
					{
						id: 6,
						"name": "波仔6",
						"img": "6.jpg"
					},
				]
			}
		},
		methods: {
			changeCount() {
				this.count++
			},
			changeSex(temp) {
				this.danger = temp
			},

			changeImg(temp) {
				if (temp == '-') {
					this.rotationIndex--;
					// 循环逻辑
					// if (this.rotationIndex < 0) {
					// 	this.rotationIndex = this.rotation.length-1;
					// }

					// 走到头停止逻辑
					if (this.rotationIndex < 0) {
						this.rotationIndex = 0;
						this.isAlert = true;
						this.alertHide()
					}
				}
				if (temp == '+') {
					this.rotationIndex++;
					// 循环逻辑
					// if (this.rotationIndex > this.rotation.length-1) {
					// 	this.rotationIndex = 0
					// }
					if (this.rotationIndex > this.rotation.length - 1) {
						this.rotationIndex = this.rotation.length - 1;
						this.isAlert = true;
						this.alertHide()
					}
				}
				
			},
			changeImgImg1(temp){
				this.rotationIndex += temp;
				if (this.rotationIndex < 0) {
					this.rotationIndex = 0;
					this.isAlert = true;
					this.alertHide()
				}
				if (this.rotationIndex > this.rotation.length - 1) {
					this.rotationIndex = this.rotation.length - 1;
					this.isAlert = true;
					this.alertHide()
				}
			}
			alertHide() {
				var that = this
				setTimeout(function() {
					that.isAlert = false
				}, 2000)
			}
		}


	};
</script>

<!-- vue create 项目 脚手架创建 vue/cli vue.js -->

<!-- 创建html页面 引包 创建vue对象 挂载路由 定义数据 渲染数据 -->
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	h3 {
		margin: 40px 0 0;
	}

	ul {
		list-style-type: none;
		padding: 0;
	}

	li {
		display: inline-block;
		margin: 0 10px;
	}

	a {
		color: #42b983;
	}
</style>
