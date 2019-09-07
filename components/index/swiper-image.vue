<template>
	<view>
		<!-- uSwiper 快速创建swiper轮播图 -->
			
		<!-- 链接滑动 circular ，从最后一个滑动到第一个 -->
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" circular>
			<block v-for="(item,index) in resdata" :key="index">
				<swiper-item>
					<view class="swiper-item" @tap="event(item)">
						<!-- lazy-load 懒加载 -->
						<!-- 写一个具体的图片高度会流畅 -->
						<image :src="item.src" 
						lazy-load
						style="height:350upx;"
						></image>
					</view>
				</swiper-item>
			</block>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		props:{ // 父向子传数据，调用子组件
			resdata:Array
		},
		methods: {
			event(item){
				console.log("点击了轮播图")
			}
		}
	}
</script>

<style>

</style>
