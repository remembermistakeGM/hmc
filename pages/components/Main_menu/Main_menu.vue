<template>
	<!-- 返回主菜单按钮 -->
	<view class="main_menu" @click="backMenu">
		<image src="../../../static/menu.png"></image>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			backMenu(){
			
				uni.navigateTo({
					 url: '/pages/index/index'
				});
			}
		}
	}
</script>

<style>
	.main_menu{
		background-color: #009688;
		width: 80rpx;
		height: 80rpx;
		border-radius: 10rpx;
		padding: 20rpx;
		position: fixed;
		top: 160rpx;
		left: 10rpx;
		z-index: 999;
	}
	.main_menu image{
		width: 100%;
		height: 100%;
	}
</style>
