<template>
  <view class="goodsWarehousing">
    <!-- 商品入库	 -->

    <!-- 返回主菜单按钮 -->
    <main_menu></main_menu>

    <view class="top_cell">
      <view class="top_cell_left">
        <button>订货单入库</button>
        <button>调货入库</button>
        <button>批量商品表入库</button>
        <button>excel模板下载</button>
      </view>
      <view class="search_box">
        <input placeholder="请输入商品名称或首字母" />
      </view>
      <view class="top_cell_right">
        <button>操作记录</button>
      </view>
    </view>

    <!-- 商品分类 -->
    <classify></classify>

    <!-- 商品列表 -->
    <view class="goods_group">
      <view class="goods_item" @click="onShowMask"  v-for="(item, index) in list" :key="index">
		<view class="goods_cell">
        <view class="goods_imgs">
			<image v-if="item.image" :src="item.image"></image>
			<image v-else src="../../static/noimg.png"></image>

		</view>
        <view class="goods_name">{{ item.goodsname }}</view>
        <view class="goods_inven">库存：<text>{{ item.inventory}}</text>{{ item.unit }}</view>
	</view>
      </view>
    </view>
<!-- 弹出层 -->
<view class="center" v-if="isShowMask" >
	<view class="mask_main" :class="{'modal': 'isShowMask'}">
	<view class="mask_title">商品入库</view>
	<view class="mask_text1">小龙虾</view>
	<view class="mask_text2">当前库存：20斤</view>
	<view class="radio_group">
		<text class="radio_title">选择入库方式：</text>
		<radio-group @change="radioChange" class="radio_group_item">
			<label class="uni-list-cell uni-list-cell-pd radio_cell" v-for="(item, index) in items" :key="item.value">
				<view>
					<radio :value="item.value" :checked="index === current" />
				</view>
				<view>{{item.name}}</view>
			</label>
		</radio-group>
	</view>
	<view class="mask_input"><input class="uni-input" type="number" focus placeholder="请输入库存" /></view>
	<view class="onsubmit"><button>确认</button></view>
</view> 
<view class="mask_bg" @click="onClose"></view>
</view>
	


  </view>
</template>

<script>
import main_menu from "../components/Main_menu/Main_menu.vue";
import classify from "../components/classify/classify.vue";

export default {
  components: {
    main_menu,
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
		 current: 0,//选中状态
		 isShowMask:false,//弹出层状态		
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
    };
  },
  methods: {
	radioChange: function(evt) {
            for (let i = 0; i < this.items.length; i++) {
                if (this.items[i].value === evt.detail.value) {
                    this.current = i;
                    break;
                }
            }
        },
		//打开弹出层
		onShowMask(){
			this.isShowMask = true

			
		},
		// 关闭弹出层
		onClose(){
			this.isShowMask = false
			
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

.mask_main {
	position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 1000rpx;
    height: 800rpx;
	z-index: 9999;
	background-color: #fff;
	border-radius: 18rpx;
	
}
.mask_bg{
	position: fixed;
	top: 0;
	left: 0;
	bottom: 0;
	right: 0;
	background-color: rgba(000, 000, 000, .5);
	z-index: 9998;
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
}
.mask_main{
	padding: 20rpx;
}
.mask_input input{
	 	padding: 20rpx;
		border: 1px solid #009688;
		border-radius: 20rpx;
		margin: 50rpx;
		font-weight: bold;
		line-height: 3rem;
		font-size: 1.3rem;
		
}
@keyframes scaleUp {
	0% {
	  transform: scale(0.8) translateY(500px);
	  opacity: 0;
	}
	100% {
	  transform: scale(1) translateX(-50%)  translateY(-50%);
	  opacity: 1;
	}
  }
 
  .modal {
	animation: scaleUp 0.5s cubic-bezier(0.165, 0.84, 0.44, 1) forwards;
  }
.onsubmit button{
	background-color: #009688;
	color: #fff;
	margin: 20rpx 100rpx;

}
</style>
