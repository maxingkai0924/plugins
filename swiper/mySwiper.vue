<template>
	<div class='swiper-containe' :style='styles'>
	    <div class='swiper' :style='{left:left+"px"}'>
			<slot></slot>
	    </div>
		<div class='point' v-if="pointhas">
		     <div class='swiper-point' @click='handlerPoint(index+1)' :class='{active:num==index+1}' v-for='(item,index) in imgList' :key='index'></div>
		</div>
		<div class='swiper-tool-left' v-if="toolhas" @click='handlderLeft'>
			<img :src="imgLeftUrl" alt="良">
		</div>
		<div class='swiper-tool-right' v-if="toolhas" @click='handlderRight'>
			<img :src="imgRightUrl" alt="优">
		</div>
	</div> 
</template>

<script>
	export default{
		name: 'mySwiper',
		props: {
			pointhas:{
				type:Boolean,
				default:false
			},
			toolhas:{
				type:Boolean,
				default:false
			},
			width: {
		        type:Number,
				default:600
			},
			height:{
				type:Number,
				default:400
			},
			imgList: {
				type: Array,
			}
		},
		data() {
			return {
				left: 0,
				num: 1,
		        styles:{
					height:this.height+'px',
					width:this.width+'px'
				},
				time:null,
				setTime:5000,
				boxWidth:this.width,
				imgLeftUrl:require('./left.png'),
				imgRightUrl:require('./right.png')
			}
		},
		methods: {
			motionTime() {
				let imgLength = this.imgList.length;
				clearInterval(this.time);  //每次清除定时器
				this.time = setInterval(() => {
					this.num++
					if (this.num > imgLength) {
						this.num = 1;
						this.left = 0;
					} else {
						this.left += -this.width;
					}
		
				}, this.setTime)
		
			},
			handlerPoint(data){  
				clearInterval(this.time);  //每次清除定时器
				this.num = data;
				this.left = -this.width*(data-1);
				this.$emit('handlerPoint',this.num);
			},
			handlderLeft(){
				let imgLength = this.imgList.length;
				clearInterval(this.time);   //每次清除定时器
				this.num--
				if (this.num <1) {
					this.num = this.imgList.length;
					console.log(this.boxWidth)
					this.left =-this.boxWidth*(this.imgList.length-1);
				} else {
					this.left += this.width;
				}
				this.$emit('handlderLeft',this.num);
				this.motionTime();
			},
			handlderRight(){
				let imgLength = this.imgList.length;; 
				clearInterval(this.time);   //每次清除定时器
				this.num++
				if (this.num > imgLength) {
					this.num = 1;
					this.left = 0;
				} else {
					this.left += -this.width;
				}
				this.$emit('handlderRight',this.num);
				this.motionTime();
			}
		},
		mounted() {
			this.motionTime();
		},
		components: {
			
		}
	}
</script>

<style lang="scss" scoped>
	.swiper-containe {
		overflow: hidden;
		position: relative;
		margin-left: 100px;
	}
	.point{
	   position: absolute;
	   right:10px;
	   bottom:15px;
	}
	.point .swiper-point{
	   width:10px;
	   height:10px;
	   border-radius:50%;
	   background:#000;
	   float: left;
	   margin-left:6px;
	   cursor:pointer;
	}
	.swiper-point.active{
		background:#fff;
	}
	.swiper-tool-left{
	   position: absolute;
	   top:43%;
	   left:10px;
	   cursor: pointer;
	   padding:10px 5px;			   
	   background:rgba(0,125,219,0.2);
	}
	.swiper-tool-right{
	   position: absolute;
	   top:43%;
	   right:10px;
	   cursor: pointer;
	   padding:10px 5px;
	   background:rgba(0,125,219,0.2);
	}
	.swiper {
		/* width:300px; */
		width: 9999999999px;
		height: 100%;
		position: absolute;
		top: 0;
		left: 0;
		transition: all 0.5s;
	}


</style>
