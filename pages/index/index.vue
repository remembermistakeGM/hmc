<template>

	<view class="content">
	
			<view class="home_title">
				菜单功能
			</view>
			<view class="home_nav_group">
			<navigator  url="/pages/inventory/inventory" class="nav_item_url">
					<view class="nav_item color1">
						<image src="../../static/xiaoshou.png"></image>
						<text>库存盘点</text>
					</view>	
			</navigator>
			<navigator  url="/pages/goodsWarehousing/goodsWarehousing" class="nav_item_url">
					<view class="nav_item color2">
						<image src="../../static/ruku.png"></image>
						<text>商品入库</text>
					</view>	
			</navigator>
				<navigator  url="" class="nav_item_url">
						<view class="nav_item color3">
							<image src="../../static/xiadan.png"></image>
							<text>收银台</text>
						</view>	
				</navigator>
				<navigator  url="" class="nav_item_url">
						<view class="nav_item color4">
							<image src="../../static/jg.png"></image>
							<text>价格管理</text>
						</view>	
				</navigator>
				<navigator  url="" class="nav_item_url">
						<view class="nav_item color5">
							<image src="../../static/md.png"></image>
							<text>门店营销</text>
						</view>	
				</navigator>
				<navigator  url="" class="nav_item_url">
						<view class="nav_item color6">
							<image src="../../static/jh.png"></image>
							<text>进货</text>
						</view>	
				</navigator>
				<navigator  url="" class="nav_item_url">
						<view class="nav_item color7">
							<image src="../../static/bh.png"></image>
							<text>订货申请</text>
						</view>	
				</navigator>
				<navigator  url="" class="nav_item_url">
						<view class="nav_item color8">
							<image src="../../static/dh.png"></image>
							<text>调货</text>
						</view>	
				</navigator>
				<navigator  url="" class="nav_item_url">
						<view class="nav_item color9">
							<image src="../../static/ddjl.png"></image>
							<text>订单记录</text>
						</view>	
				</navigator>
				<navigator  url="" class="nav_item_url">
						<view class="nav_item color10">
							<image src="../../static/wdhy.png"></image>
							<text>会员管理</text>
						</view>	
				</navigator>
				<navigator  url="" class="nav_item_url">
						<view class="nav_item color11">
							<image src="../../static/jianshao.png"></image>
							<text>交班</text>
						</view>	
				</navigator>
			</view>
			
			
	</view>
</template>

<script>


	export default {
    data() {
        return {};
    },
    onLoad() {
    },
    methods: {},
    components: {  }
}
</script>

<style scoped>
	.home_title{
		font-weight: bold;
		text-align: center;
		line-height: 3rem;
		font-size: 1.3rem;
		position: relative;
		padding-top: 40rpx;
	}
		
	.home_title::after{
		content: '';
		position: absolute;
		bottom: 10rpx;
		left: 0rpx;
		width: 100%;
		bottom: 0rpx;
		background-color: #e5e5e5;
		height: 2rpx;
	}
	
	.home_nav_group{
		display: flex;
		flex-wrap: wrap;
		
	}
	.nav_item_url{
		width: 25%;
		margin-top: 20rpx;
	}
	.nav_item{
		width: 100%;
		margin: 20rpx;
	}
	.nav_item image{
		width: 160rpx;
		height: 160rpx;
		display: block;
		text-align: center;
		margin: 10rpx auto;
		padding: 20rpx;
		border-radius: 20rpx;
	}
	.nav_item text{
		text-align: center;
		display: block;
		font-weight: bold;
	}
	.color1 image{
		background-color: #f3b94f;
	}
	.color2 image{
		background-color: #12f8ed;
	}
	.color3 image{
		background-color: #40d19a;
	}
	.color4 image{
		background-color: #87240f;
	}
	.color5 image{
		background-color: #898a8c;
	}
	.color6 image{
		background-color: #a77c38;
	}
	.color7 image{
		background-color: #907c75;
	}
	.color8 image{
		background-color: #ae730f;
	}
	.color9 image{
		background-color: #101c34;
	}
	.color10 image{
		background-color: #40d19a;
	}
	.color11 image{
		background-color: #101c34;
	}
</style>
