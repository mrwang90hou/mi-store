<template>
	<view class="uni-tab-bar">
		<!-- 横向滚动导航部分 -->
		<scroll-view id="tab-bar" class="uni-swiper-tab" scroll-x :scroll-left="scrollLeft">
			<view
				v-for="(tab, index) in tabBars"
				:key="tab.id"
				class="swiper-tab-list"
				:class="tabIndex == index ? 'active' : ''"
				:id="tab.id"
				:data-current="index"
				@click="tapTab(index)"
			>
				<view class="tabitems">{{ tab.name }}</view>
			</view>
		</scroll-view>

		<!-- 列表 -->
		<swiper :current="tabIndex" class="swiper-box" :duration="300" @change="changeTab">
			<swiper-item v-for="(tab, index1) in newsitems" :key="index1">
				<scroll-view class="list" scroll-y @scrolltolower="loadMore(index1)">
					<!-- 内容 -->

					<!-- index模板 -->
					<template v-if="tabBars[index1].template === 'index'">
						<block v-for="(v, i) in tab.data" :key="i">
							<!-- 循环tab的data -->

							<template v-if="v.type === 'swiper'">
								<!-- // 判断类型是否等于swiper 然后渲染 -->
								<!-- 轮播图组件 ! -->
								<swiper-image :resdata="v.data" />
							</template>
							<template v-else-if="v.type === 'indexNavs'">
								<!-- 首页分类 ! -->
								<index-nav :resdata="v.data" />

								<!-- 全局分割线 -->
								<divider />
							</template>

							<template v-else-if="v.type === 'threeAdv'">
								<!-- 三图广告 -->
								<three-adv :resdata="v.data" />

								<!-- 全局分割线 -->
								<divider />
							</template>

							<template v-else-if="v.type === 'oneAdv'">
								<!-- 卡片组件 -->
								<!-- 大图广告位 -->
								<card :headerTitle="v.data.title" :bodyCover="v.data.cover" />
								<!-- <card :showHead="false">
								<block slot="title"></block>			
								<image src="/static/images/bg.jpg" mode="widthFix"></image>
							</card> -->
							</template>

							<template v-else-if="v.type === 'list'">
								<!-- 公共列表组件 (750 - 5) / 2 = 372.5upx -->
								<view class="row j-sb">
									<block v-for="(vlist, listindex) in v.data" :key="listindex"><common-list :item="vlist" :index="listindex"></common-list></block>
								</view>
							</template>
						</block>
					</template>

					<!-- special模板 -->
					<template v-if="tabBars[index1].template === 'special'">
						<block v-for="(v, i) in tab.data" :key="i">
							<template v-if="v.type === 'swiper'">
								<!-- // 判断类型是否等于swiper 然后渲染 -->
								<!-- 轮播图组件 ! -->
								<swiper-image :resdata="v.data" />
							</template>
							<template v-else-if="v.type === 'indexNavs'">
								<!-- 首页分类 ! -->
								<index-nav :resdata="v.data" />

								<!-- 全局分割线 -->
								<divider />
							</template>

							<template v-else-if="v.type === 'list'">
								<!-- 公共列表组件 (750 - 5) / 2 = 372.5upx -->
								<card headerTitle="热卖爆品">
									<view class="row j-sb">
										<block v-for="(vlist, listindex) in v.data" :key="listindex">
											<common-list :item="vlist" :index="listindex"></common-list>
										</block>
									</view>
								</card>
								
							</template>
						</block>
					</template>

					<!-- 每个页面的加载更多 -->
					<view class="uni-tab-bar-loading">{{ tab.loadingText }}</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>
<script>
import swiperImage from '@/components/index/swiper-image.vue';
import indexNav from '@/components/index/index-nav.vue';
import threeAdv from '@/components/index/three-adv.vue';
import card from '@/components/common/card.vue';
import commonList from '@/components/common/common-list.vue';

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
			scrollLeft: 0,
			isClickChange: false,
			tabIndex: 0,
			newsitems: [],
			tabBars: [
				{
					name: '关注',
					id: 'guanzhu',
					template: 'index'
				},
				{
					name: '推荐',
					id: 'tuijian',
					template: 'special'
				},
				{
					name: '体育',
					id: 'tiyu'
				},
				{
					name: '热点',
					id: 'redian'
				},
				{
					name: '财经',
					id: 'caijing'
				},
				{
					name: '娱乐',
					id: 'yule'
				},
				{
					name: '军事',
					id: 'junshi'
				},
				{
					name: '历史',
					id: 'lishi'
				},
				{
					name: '本地',
					id: 'bendi'
				}
			]
		};
	},
	// 页面加载的时候 加载数据
	onLoad() {
		this.newsitems = this.randomfn();
	},
	methods: {
		// 加载更多
		loadMore(e) {
			setTimeout(() => {
				this.addData(e);
			}, 1200);
		},
		// 模拟数据
		addData(e) {
			// 拿到当前索引e
			if (this.newsitems[e].data.length > 30) {
				this.newsitems[e].loadingText = '没有更多了';
				return;
			}
			let arr = [
				{
					type: 'swiper', // 轮播图  根据类型使用不同组件渲染
					data: [{ src: '../../static/images/demo/demo4.jpg' }, { src: '../../static/images/demo/demo4.jpg' }, { src: '../../static/images/demo/demo4.jpg' }]
				},
				{
					type: 'indexNavs', // 8个选项图标 根据类型使用不同组件渲染
					data: [
						{ src: '../../static/images/indexnav/1.png', text: '新品发布' },
						{ src: '../../static/images/indexnav/2.gif', text: '小米众筹' },
						{ src: '../../static/images/indexnav/3.gif', text: '以旧换新' },
						{ src: '../../static/images/indexnav/4.gif', text: '一分拼团' },
						{ src: '../../static/images/indexnav/5.gif', text: '超值特卖' }
					]
				},
				{
					type: 'list', // 根据类型使用不同组件渲染
					data: [
						{
							cover: '../../static/images/demo/list/1.jpg',
							title: '米家空调',
							desc: '1.5匹变频',
							oprice: 2699,
							pprice: 1399
						},
						{
							cover: '../../static/images/demo/list/1.jpg',
							title: '米家空调',
							desc: '1.5匹变频',
							oprice: 2699,
							pprice: 1399
						},
						{
							cover: '../../static/images/demo/list/1.jpg',
							title: '米家空调',
							desc: '1.5匹变频',
							oprice: 2699,
							pprice: 1399
						},
						{
							cover: '../../static/images/demo/list/1.jpg',
							title: '米家空调',
							desc: '1.5匹变频',
							oprice: 2699,
							pprice: 1399
						}
					]
				}
			];
			this.newsitems[e].data = [...this.newsitems[e].data, ...arr]; // 暂时不明白这句代码是什么意思
			console.log(JSON.stringify(this.newsitems[e].data));
		},
		// 改变tab
		async changeTab(e) {
			let index = e.target.current;
			if (this.newsitems[index].data.length === 0) {
				this.addData(index);
			}
			if (this.isClickChange) {
				this.tabIndex = index;
				this.isClickChange = false;
				return;
			}
			let tabBar = await this.getElSize('tab-bar'),
				tabBarScrollLeft = tabBar.scrollLeft;
			let width = 0;

			for (let i = 0; i < index; i++) {
				let result = await this.getElSize(this.tabBars[i].id);
				width += result.width;
			}
			let winWidth = uni.getSystemInfoSync().windowWidth,
				nowElement = await this.getElSize(this.tabBars[index].id),
				nowWidth = nowElement.width;
			if (width + nowWidth - tabBarScrollLeft > winWidth) {
				this.scrollLeft = width + nowWidth - winWidth;
			}
			if (width < tabBarScrollLeft) {
				this.scrollLeft = width;
			}
			this.isClickChange = false;
			this.tabIndex = index; //一旦访问data就会出问题
		},
		getElSize(id) {
			//得到元素的size
			return new Promise((res, rej) => {
				uni.createSelectorQuery()
					.select('#' + id)
					.fields(
						{
							size: true,
							scrollOffset: true
						},
						data => {
							res(data);
						}
					)
					.exec();
			});
		},
		async tapTab(e) {
			//点击tab-bar
			let tabIndex = e;
			if (this.newsitems[tabIndex].data.length === 0) {
				this.addData(tabIndex);
			}
			if (this.tabIndex === tabIndex) {
				return false;
			} else {
				let tabBar = await this.getElSize('tab-bar'),
					tabBarScrollLeft = tabBar.scrollLeft; //点击的时候记录并设置scrollLeft
				this.scrollLeft = tabBarScrollLeft;
				this.isClickChange = true;
				this.tabIndex = tabIndex;
			}
		},
		// 生成随机数据
		randomfn() {
			let ary = [];
			// 拿到tabbars的长度，根据长度生成页面
			let tablength = this.tabBars.length;
			for (let i = 0; i < tablength; i++) {
				let aryItem = {
					loadingText: '加载更多...',
					data: []
				};
				// 给页面添加数据
				if (this.tabBars[i].template === 'index') {
					aryItem.data = [
						{
							type: 'swiper', // 轮播图  根据类型使用不同组件渲染
							data: [{ src: '../../static/images/demo/demo4.jpg' }, { src: '../../static/images/demo/demo4.jpg' }, { src: '../../static/images/demo/demo4.jpg' }]
						},
						{
							type: 'indexNavs', // 8个选项图标 根据类型使用不同组件渲染
							data: [
								{ src: '../../static/images/indexnav/1.png', text: '新品发布' },
								{ src: '../../static/images/indexnav/2.gif', text: '小米众筹' },
								{ src: '../../static/images/indexnav/3.gif', text: '以旧换新' },
								{ src: '../../static/images/indexnav/4.gif', text: '一分拼团' },
								{ src: '../../static/images/indexnav/5.gif', text: '超值特卖' },
								{ src: '../../static/images/indexnav/6.gif', text: '小米秒杀' },
								{ src: '../../static/images/indexnav/7.gif', text: '真心想要' },
								{ src: '../../static/images/indexnav/8.gif', text: '电视热卖' },
								{ src: '../../static/images/indexnav/9.gif', text: '家电热卖' },
								{ src: '../../static/images/indexnav/10.gif', text: '米粉卡' }
							]
						},
						{
							type: 'threeAdv',
							data: {
								big: {
									src: '/static/images/demo/demo1.jpg'
								},
								smallTop: {
									src: '/static/images/demo/demo2.jpg'
								},
								smallBottom: {
									src: '/static/images/demo/demo2.jpg'
								}
							}
						},
						{
							type: 'oneAdv',
							data: {
								title: '每日精选',
								cover: '/static/images/demo/demo2.jpg'
							}
						},
						{
							type: 'list', // 根据类型使用不同组件渲染
							data: [
								{
									cover: '../../static/images/demo/list/1.jpg',
									title: '米家空调',
									desc: '1.5匹变频',
									oprice: 2699,
									pprice: 1399
								},
								{
									cover: '../../static/images/demo/list/1.jpg',
									title: '米家空调',
									desc: '1.5匹变频',
									oprice: 2699,
									pprice: 1399
								},
								{
									cover: '../../static/images/demo/list/1.jpg',
									title: '米家空调',
									desc: '1.5匹变频',
									oprice: 2699,
									pprice: 1399
								},
								{
									cover: '../../static/images/demo/list/1.jpg',
									title: '米家空调',
									desc: '1.5匹变频',
									oprice: 2699,
									pprice: 1399
								}
							]
						}
					];
				}
				ary.push(aryItem);
			}
			return ary;
		}
	}
};
</script>

<style>
.uni-tab-bar-loading {
	text-align: center;
	font-size: 28upx;
	color: #999;
}
.tabitems {
	display: inline-block;
	width: 75upx;
	border-bottom: 5upx solid rgba(0, 0, 0, 0);
}
.active .tabitems {
	border-bottom: 5upx solid #fd6801;
}
</style>
