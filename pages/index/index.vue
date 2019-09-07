<template>
	<view >
	
		<!-- 轮播图组件 ! -->
		<swiper-image :resdata="swipers" />
	
		<!-- 首页分类 ! -->
		<index-nav :resdata="indexNvas" />
		
		<!-- 全局分割线 -->
		<divider />
		
		<!-- 三图广告 -->
	 	<three-adv :resdata="threeAdv" />
		
		<!-- 全局分割线 -->
		<divider />
		
		<!-- 卡片组件 -->
		<!-- 大图广告位 -->
		<card headerTitle="每日精选" bodyCover="../../static/images/demo/demo4.jpg" />
		<!-- <card :showHead="false">
			<block slot="title"></block>			
			<image src="/static/images/bg.jpg" mode="widthFix"></image>
		</card> -->
		
		<!-- 公共列表组件 (750 - 5) / 2 = 372.5upx -->
		<view class="row j-sb">
			<block v-for="(item,index) in commonList" :key="index">
				<common-list :item="item" :index="index"></common-list>
			</block>
		</view>
		
		
		
	</view>
</template>

<script>
	import swiperImage from '@/components/index/swiper-image.vue'
	import indexNav from '@/components/index/index-nav.vue'
	import threeAdv from '@/components/index/three-adv.vue'
	import card from "@/components/common/card.vue"
	import commonList from '@/components/common/common-list.vue'

	
	export default {
		components: {
			swiperImage,
			indexNav,
			threeAdv,
			card,
			commonList
		},
		data() {
			return {
				// 轮播图数据
				swipers:[
					{src:"../../static/images/demo/demo4.jpg"},
					{src:"../../static/images/demo/demo4.jpg"},
					{src:"../../static/images/demo/demo4.jpg"}
				],
				indexNvas:[
					{src:"../../static/images/indexnav/1.png",text:"新品发布"},
					{src:"../../static/images/indexnav/2.gif",text:"小米众筹"},
					{src:"../../static/images/indexnav/3.gif",text:"以旧换新"},
					{src:"../../static/images/indexnav/4.gif",text:"一分拼团"},
					{src:"../../static/images/indexnav/5.gif",text:"超值特卖"},
					{src:"../../static/images/indexnav/6.gif",text:"小米秒杀"},
					{src:"../../static/images/indexnav/7.gif",text:"真心想要"},
					{src:"../../static/images/indexnav/8.gif",text:"电视热卖"},
					{src:"../../static/images/indexnav/9.gif",text:"家电热卖"},
					{src:"../../static/images/indexnav/10.gif",text:"米粉卡"},
				],
				threeAdv:{
					big:{
						src:"/static/images/demo/demo1.jpg"
					},
					smallTop:{
						src:"/static/images/demo/demo2.jpg"
					},
					smallBottom:{
						src:"/static/images/demo/demo2.jpg"
					}
				},
				commonList:[
					{
						cover:"../../static/images/demo/list/1.jpg",
						title:"米家空调",
						desc:"1.5匹变频",
						oprice:2699,
						pprice:1399
					},
					{
						cover:"../../static/images/demo/list/1.jpg",
						title:"米家空调",
						desc:"1.5匹变频",
						oprice:2699,
						pprice:1399
					},
					{
						cover:"../../static/images/demo/list/1.jpg",
						title:"米家空调",
						desc:"1.5匹变频",
						oprice:2699,
						pprice:1399
					},
					{
						cover:"../../static/images/demo/list/1.jpg",
						title:"米家空调",
						desc:"1.5匹变频",
						oprice:2699,
						pprice:1399
					},
				]
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
