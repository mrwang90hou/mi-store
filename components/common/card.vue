<template>
	
	<!-- 写基础卡片组件 -->
	<view class="card">
		<!-- header -->
		<!-- 判断showHead传的值，来控制显示隐藏 -->
		<view v-if="showHead" class="p-2 border-bottom main-border-color">
			<slot name="title">
				<!-- 判断如果headerTitlem没有传任何值就不显示 -->
				<text v-if="headerTitle" class="font-md font-weight">{{headerTitle}}</text>
			</slot>
		</view>
		
		<!-- body -->
		<view>
			<!-- 如果bodyCover有值的话，就显示 -->
			<image v-if="bodyCover" :src="bodyCover" 
			mode="widthFix"></image>
			<!-- 插槽 -->
			<slot />
		</view>
		
		
	</view>
	
</template>

<script>
	export default{
		props:{
			// 头部标题
			headerTitle:String,
			// 封面图
			bodyCover:String,
			// 是否显示头部
			showHead:{
				type:Boolean,
				default:true
			}
		},
		
	}
</script>

<style>
</style>
