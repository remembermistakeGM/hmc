<template>
  <view class="priceAdmin">
    <!-- 商品入库	 -->

    <view class="top_cell">
      <view class="top_cell_left">

      </view>
      <view class="search_box">
        <input placeholder="请输入商品名称或首字母" />
      </view>
      <view class="top_cell_right" @click="goLink">
  
      </view>
    </view>

    <!-- 商品分类 -->
    <classify :classifylist="classify"></classify>

    <!-- 商品列表 -->
    <view class="goods_group">
      <view class="goods_item" @click="onShowMask"  v-for="(item, index) in list" :key="index">
		<view class="goods_cell">
        <view class="goods_imgs">
			<image v-if="item.image" :src="item.image"></image>
			<image v-else src="../../static/noimg.png"></image>

		</view>
        <view class="goods_name">{{ item.goodsname }}</view>
        <view class="goods_inven">当前价格：<text>{{ item.inventory}}</text></view>
        <view class="goods_inven">当前会员价格：<text>{{ item.inventory}}</text></view>

	</view>
      </view>
    </view>

<!-- 点击商品入库弹窗 -->
<main-mask :maskStatus="isShowMask" :mWidth="1000" :mHeight="800" @onClose="onClose">
  <template v-slot:content>
      <view class="mask_title">修改价格</view>
      <view class="mask_text1">小龙虾</view>
      <view class="mask_text2">最近入库单价: ￥10.00</view>
      <view class="mask_text2">成本均价: ￥10.00</view>
      <view class="mask_text2">最近入库单价: ￥10.00</view>
      <view class="mask_input"><text>加价率</text><input class="uni-input" type="number" focus placeholder="请输入加价率" /></view>
      <view class="mask_input"><text>售价</text><input class="uni-input" type="number" focus placeholder="请输入售价" /></view>
      <view class="mask_input"><text>会员价</text><input class="uni-input" type="number" focus placeholder="请输入会员价" /></view>

      <view class="onsubmit"><button>确认</button><button @click="onClose1">取消</button></view>


  </template>

</main-mask>


  </view> 
</template>
<script>

import classify from "../components/classify/classify.vue";
import mainMask from "../components/mainMask/mainMask.vue";

export default {
  components: {
    mainMask,
    classify,
  },
  data() {
    return {
		//选择框
		items:[
			{
                    value: '1',
                    name: '最终库存',
                 
                },
                {
                    value: '2',
                    name: '添加库存'
                },
		  ],
	
		 isShowMask:false,//商品入库弹出层状态，
     mWidth:1000,
     mHeight:800,

      list: [
        {
          id: "458",
          goodsname: "波士顿大龙虾",
          image:
            "https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-12-16/639c1c17c3715.png",
          inventory: 1.01,
          unit: "斤",
        },
        {
          id: "458",
          goodsname: "波士顿大龙虾",
          image:"",
          inventory: 1.01,
          unit: "斤",
        },
        {
          id: "458",
          goodsname: "波士顿大龙虾",
          image:
            "https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-12-16/639c1c17c3715.png",
          inventory: 1.01,
          unit: "斤",
        },
        {
          id: "458",
          goodsname: "波士顿大龙虾",
          image:
            "https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-12-16/639c1c17c3715.png",
          inventory: 1.01,
          unit: "斤",
        },
		{
          id: "458",
          goodsname: "波士顿大龙虾",
          image:
            "https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-12-16/639c1c17c3715.png",
          inventory: 1.01,
          unit: "斤",
        },
		{
          id: "458",
          goodsname: "波士顿大龙虾",
          image:
            "https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-12-16/639c1c17c3715.png",
          inventory: 1.01,
          unit: "斤",
        },
		{
          id: "458",
          goodsname: "波士顿大龙虾",
          image:
            "https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-12-16/639c1c17c3715.png",
          inventory: 1.01,
          unit: "斤",
        },
		{
          id: "458",
          goodsname: "波士顿大龙虾",
          image:
            "https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-12-16/639c1c17c3715.png",
          inventory: 1.01,
          unit: "斤",
        },
      ],
      classify: [
                    { title: "全部",  },
                    { title: "蟹类",  },
			 ],
     
    };
  },
  methods: {
		//打开商品入库弹出层
		onShowMask(){
			this.isShowMask = true
		},
		// 关闭商品入库弹出层
		onClose(e){
			this.isShowMask = e
		},
    onClose1(){
			this.isShowMask =false
      
    },
    goLink(){
      uni.navigateTo({
         url: '/pages/goodsWarehousing/WhRecording'
      });
    }
    

  },
};
</script>

<style scoped>
.top_cell {
  padding: 40rpx 20rpx;
  background-color: #e6e6e6;
  display: flex;
  justify-content: space-between;
  align-items: center;
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
.top_cell_left {
  display: flex;
  margin-left: 100rpx;
}
.top_cell_left button {
  margin-left: 18rpx;
  background-color: #009688;
  color: #fff;
  font-weight: bold;
  font-size: 0.9rem;
  line-height: 2.2rem;
  height: 2.2rem;
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
.goods_group{
	display: flex;
	flex-wrap:wrap;
}
.goods_group .goods_item{
	width: 16.66666667%;
}
.goods_group .goods_cell{
	margin:40rpx;
	border: 1rpx solid#009688;
	border-radius: 10rpx;

}
.goods_group .goods_item .goods_cell .goods_imgs image{
	width: 200rpx;
	height: 200rpx;
	display: block;
	margin: 10rpx auto;
	border-radius: 10rpx;
}
.goods_group .goods_item .goods_cell .goods_name{
	font-weight: bold;
    font-size: 1rem;
    margin-top: 10rpx;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
	text-align: center;
}
.goods_inven{
	font-size: 0.9rem;
	margin: 10rpx;
}
.goods_inven text{
	font-weight: bold;
}


.mask_title{
	font-weight: bold;
	text-align: center;
	margin: 30rpx auto;
}
.radio_group{

	display: flex;
	align-items: center;
}
.radio_group_item{
	display: flex;
}
.radio_cell{
	display: flex;
	margin-left: 30rpx;
}
.mask_text2{
	margin: 20rpx 0;
  font-size: 0.8rem;
}
.mask_main{
	padding: 20rpx;
}
.mask_input{
  display: flex;
  align-items: center;
}
.mask_input text{
  width: 50px;
}
.mask_input input{
	 	padding:10rpx;
		border: 1px solid #009688;
		border-radius: 6rpx;
		margin:20rpx;
		font-weight: bold;
		line-height: 2rem;
		font-size: 1rem;
}
.onsubmit {
  display: flex;
  justify-content: center;
}
.onsubmit button{
	background-color: #009688;
	color: #fff;
	margin: 20rpx 50rpx;
  width: 200rpx;
 

}
.onsubmit button:last-child{
  background-color: #666;
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
	padding: 0rpx 20rpx;
  font-size: 0.95rem;

}
.dhd_bottom{
  display: flex;
  justify-content: center;
  padding: 60rpx;
}
.dhd_bottom button{
  background-color: #009688;
	color: #fff;
  width: 160rpx;
}
.dhd_bottom button:nth-child(2){
  background-color: #c5c5c5;
	color: rgb(0, 0, 0);


}
</style>
