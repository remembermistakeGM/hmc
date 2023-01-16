<template>
	<view class="inventory">
	
		<view class="top_cell">
			<view></view>
			<view class="search_box">
				<input placeholder="请输入商品名称或首字母">
			</view>
			<view class="top_cell_right">
				<button>一键清零</button>
				<button>导出</button>
				<button>操作记录</button>
			</view>
		</view>
		<!-- 分类 -->
		<classify></classify>

	<view class="tables">
		<view class="thead">
			<view class="tr">
				<view class="td">序号</view>
				<view class="td">商品名称</view>
				<view class="td">商品图片</view>
				<view class="td">当前库存</view>
				<view class="td">损耗</view>
				<view class="td">减耗成本均价</view>
				<view class="td">近期库存盘点时间</view>
				<view class="td">操作</view>
			</view>
		</view>
		<view class="tbody">
		<view class="tr"  v-for="(list,index) in lists" :key="index">
			<view class="td">{{list.id}}</view>
			<view class="td">{{list.goodsname}}</view>
			<view class="td"><image class="tdimg" :src="list.image"></image></view>
			<view class="td">{{list.inventory}}</view>
			<view class="td">{{list.sh}}</view>
			<view class="td">{{list.cbjj}}</view>
			<view class="td">{{list.pdtime}}</view>
			<view class="td">
				<view class="td_icon">
				<text class="iconfont icon-xiugai07"></text>
				<text class="iconfont icon-frost"></text>
				<text class="iconfont icon-shanchu"></text>
				</view>

			</view>

			
		</view>	
		
		</view>

	</view>

	</view>
</template>

<script>
import classify from '../components/classify/classify.vue';

export default {
	components: {
		classify
	},
	data() {
		return {
			
			lists:[
              {id: '458', goodsname: '波士顿大龙虾',image: "https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-12-16/639c1c17c3715.png",inventory: 1.01,sh:0,cbjj:0,pdtime:"2022-12-29 17:37:06" },
              {id: '458', goodsname: '波士顿大龙虾',image: "https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-12-16/639c1c17c3715.png",inventory: 1.01,sh:0,cbjj:0,pdtime:"2022-12-29 17:37:06" },
              {id: '458', goodsname: '波士顿大龙虾',image: "https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-12-16/639c1c17c3715.png",inventory: 1.01,sh:0,cbjj:0,pdtime:"2022-12-29 17:37:06" },
              {id: '458', goodsname: '波士顿大龙虾',image: "https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-12-16/639c1c17c3715.png",inventory: 1.01,sh:0,cbjj:0,pdtime:"2022-12-29 17:37:06" },

			]
		}
	},
	methods: {
		
	}
}
</script>

<style scoped>
.top_cell {
	padding: 40rpx 20rpx;
	background-color: #e6e6e6;
	display: flex;
	justify-content: space-between;
}

.search_box {
	align-self: center;
	justify-content: center;
}

.search_box input {
	background-color: #fff;
	border-radius: 100rpx;
	height: 3rem;
	line-height: 3rem;
	padding: 0rpx 30rpx;
	font-weight: bold;
	font-size: 1.3rem;
}

.top_cell_right {
	display: flex;

}

.top_cell_right button {

	margin-right: 18rpx;
	background-color: #009688;
	color: #fff;
	font-weight: bold;
}

.thead .tr{
	display: flex;
	width: 100%;
	height: 3rem;
	align-items: center;
	
}
.thead .tr .td{
	background-color: #f0f0f0;
	height: 3rem;
	line-height: 3rem;
	padding: 0rpx 20rpx;
	flex: 1;
	text-align: center;
	align-items: center;
    color: #666;
}
.tbody .tr{
	display: flex;
	align-items: center;
	padding:10rpx 0rpx ;
	border-bottom: 1rpx solid #e5e5e5;
}
.tbody .tr .td{
	flex: 1;
	align-items: center;
	text-align: center;
	padding: 10rpx 20rpx;

}
.tdimg{
	width: 100rpx;
	height: 100rpx;
	border-radius: 10rpx;	
}
.td_icon{
	display: flex;
	align-items: center;	
	justify-content: center;

}
.td_icon text{
	font-size: 1.3rem;
	display: block;
	padding:0rpx 20rpx;
	color: #009688;
}
</style>
