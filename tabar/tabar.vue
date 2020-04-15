<template>
	<div class="tabar-containe" :style="width:width+'px'">
		<div class="tabar" v-for="(item, index) in data" :key="index">
			<div @click="selectMenu(item)" class="selectMenu"  :class="[activeid===item.id?'active':'']">
				<span >{{ item.name }}</span>
			</div>
			<template v-if="item.children">
				  <transition name="fade" >
				      <myTabar  v-if="selectid==item.id" @select='selectTabar' class='myTabar':menu-data="item.children"></myTabar>
				  </transition>	
			</template>
		</div>
	</div>
</template>
<script>
export default {
	name: 'myTabar',
	props: {
		menuData: {
			type: Array
		},
		width:{
			type:Number,
			default:300
		}
	},
	data(){
		 return{
			 open:false,
			 selectid:'',
			 activeid:'',
		 }
	},
	mounted() {
		console.log(this.data);
	},
	methods: {
		selectMenu(item) {
			this.open = !this.open;
			this.activeid = item.id;
			if(this.selectid==item.id){
				this.selectid='';
			}else{
				this.selectid = item.id;
			}
			this.$emit('select',item)
		},
		selectTabar(item){
			this.$emit('select',item)
		}
	},
	computed:{
		data(){
			this.menuData.forEach((item)=>{
				item['open'] = false;
			});
			return  this.menuData
		}
	}
};
</script>

<style lang="scss" scoped>
	    
        .tabar-containe{
			width:300px;
			background:#356c90;
			overflow:hidden;
			color: #fff;
		}
		.tabar .selectMenu{
			display: inline-block;
			width:100%;
			cursor: pointer;
			height:45px;
			line-height: 45px;
			padding-left: 10px;
			overflow:hidden; //超出的文本隐藏
			text-overflow:ellipsis; //溢出用省略号显示
			white-space:nowrap; //溢出不换行
		}
		.tabar .selectMenu span{
			display: inline-block;
		}
		.tabar .selectMenu.active{
			background:rgba(255,255,255,0.1)
		}
		.head {
			display: none;
		}

		.show {
			display: block;
		}
		.color {
			color: #fff;
		}
		// .myTabar span{
		// 	padding-left: 20px;
		// }
		
		.fade-enter-active{
		    transition: all 0.6s;
		}
		.fade-leave-active {
			transition: all 0.6s;
		}
		.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
		    opacity:0;
			transform: skew(10deg) translateX(10px)
		}
</style>
