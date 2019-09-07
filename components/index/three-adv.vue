<template>
	<!-- 左边w:373 h530 -->
	<!-- 右边w:375 h264 间隙2 -->
	<view class="d-flex">
		<image :src="resdata.big.src" 
		@tap="event(resdata.big)"
		lazy-load 
		style="width:373upx;height:530upx;border-right:2upx solid #f5f5f5;"
		></image>
		<view class="d-flex flex-column">
			<image :src="resdata.smallTop.src"
			@tap="event(resdata.smallTop)"
			style="width:375upx;height:264upx;border-bottom:2upx solid #f5f5f5;" mode=""></image>
			
			<image :src="resdata.smallBottom.src"
			@tap="event(resdata.smallTop)"
			style="width:375upx;height:264upx;" mode=""></image>
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			resdata:Object
		},
		methods:{
			event(obj){
				console.log(obj)
			}
		}
	}
</script>

<style>
</style>
