<template>
	<view class="market">
		<view class="margket-group">
			<view class="margket-item">
				<navigator url="/pages/market/manjian" class="margket-image">
			 	 <image src="../../static/jianshao.png"></image>.
				</navigator>
				<text>满减</text>	 
			</view>
			<view class="margket-item">
				<navigator class="margket-image" url="/pages/market/tejia">
				<image src="../../static/jianshao.png"></image>.
				</navigator>
				<text>特价</text>	
			</view>
			<view class="margket-item">
				<navigator class="margket-image" url="/pages/market/mz">
				<image src="../../static/jianshao.png"></image>.
				</navigator>
				<text>买赠</text>	
			</view>
			<view class="margket-item">
				<navigator class="margket-image" url="/pages/market/zk">
				<image src="../../static/jianshao.png"></image>.
				</navigator>
				<text>第二件折扣</text>	
			</view>

		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
.margket-group{
	display: flex;
	justify-content: center;
	flex-wrap: wrap;
	width: 50%;
	margin:36rpx auto;
}
	.margket-item{
		width: 50%;
		align-items: center;
		margin-top: 40rpx;
	}
.margket-image{
	background-color: blue;
	border-radius: 10rpx;
	padding: 30rpx;
	width:120rpx;
	height: 120rpx;
	margin: 30rpx auto;
	text-align: center;
}
.margket-image image{
	width: 90rpx;
	height: 90rpx;
	display: block;
	margin: 0rpx auto;
	margin-top: 20rpx;
} 
.margket-item text{
text-align: center;
display: block;
}
</style>
