<template>
	<view class="content">

		<view class="d-flex bg-white border-top position-fixed bottom-0 left-0 right-0" style="width: 100%;height:90upx;">
			<view class="flex-1 d-flex j-center a-center flex-column line-h">
				<view class="iconfont icon-xihuan line-h"></view>
				收藏
			</view>
			<view class="flex-1 d-flex j-center a-center flex-column line-h">
				<view class="iconfont icon-gouwuche line-h"></view>
				购物车
			</view>
			<view style="flex:2.5;" class="text-white main-bg-color d-flex j-center a-center " hover-class="main-bg-hover-color">
				加入购物车
			</view>
		</view>


	</view>
</template>

<script>
	export default {
		data() {
			return {
				show:true,
				title: 'Hello'
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50upx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
</style>
