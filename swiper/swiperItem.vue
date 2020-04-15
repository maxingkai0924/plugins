<template>
	<div class='swiper-item' :style='styles'>
	    <slot></slot>
	</div>
</template>

<script>
	export default{
		name:'swipeItem',
		props:{
			imgData:{
				type:Object,
			},
			width: {
			    type:Number,
			},
			height:{
				type:Number
			},
		},
		data(){
			return{
				 time:null,
				 styles:{
				 	height:this.height+'px',
				 	width:this.width+'px'
				 }
			}
		},
	}
</script>

<style lang="scss" scoped>
	 .swiper-item {
	 	height: 100%;
	 	float: left;
	 	position: relative;
	 }
	 
	 .swiper-item img {
	 	width: 100%;
	 	height: 100%;
	 	display: block;
	 }
	 
	 .swiper-item div {
	 	width: 100%;
	 	height: 40px;
	 	position: absolute;
	 	bottom: 0;
	 	left: 0;
	 	background: rgba(0, 0, 0, 0.6);
	 }
</style>
