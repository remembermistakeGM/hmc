<template>
  <view class="goodsWarehousing">
    <!-- 商品入库	 -->

    <view class="top_cell">
      <view class="top_cell_left">
        <button @click="onDhd">订货单入库</button>
        <button  @click="onJh">调货入库</button>
        <button>批量商品表入库</button>
        <button>excel模板下载</button>
      </view>
      <view class="search_box">
        <input placeholder="请输入商品名称或首字母" />
      </view>
      <view class="top_cell_right" @click="goLink">
        <button >操作纪录</button>
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

<!-- 点击商品入库弹窗 -->
<main-mask :maskStatus="isShowMask" :mWidth="1000" :mHeight="800" @onClose="onClose">
  <template v-slot:content>
 
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


  </template>

</main-mask>

<!-- 订货单入库弹窗 -->
<main-mask :maskStatus="isShowMaskDhd" :mWidth="1500" :mHeight="900"  @onClose="onCloseDhd">
  <template v-slot:content>
    <view class="mask_title">进货单</view>
    <view class="tables">
      <view class="thead">
        <view class="tr">
          <view class="td">商品</view>
          <view class="td">进货量</view>
          <view class="td">单位</view>
          <view class="td">实际进货量</view>
          <view class="td">上次进货价</view>
          <view class="td">上次进货量</view>
          <view class="td">备注</view>
        </view>
      </view>
      <view class="tbody">
        <scroll-view scroll-y="true" style="height:500rpx" >
      <view class="tr"  v-for="(list,index) in dhdlist" :key="index">
        <view class="td">{{list.goodsname}}</view>
        <view class="td">{{list.num}}</view>
        <view class="td">{{list.unit}}</view>
        <view class="td">{{list.sjnum}}</view>
        <view class="td">{{list.lastprice}}</view>
        <view class="td">{{list.lastnum}}</view>
        <view class="td">{{list.remark}}</view>
      </view>	
    </scroll-view>
      </view>
    </view>
    <view class="dhd_bottom"> 
      <button>确认</button>
      <button @click="onParentColseDhd">取消</button>
    </view>
  </template>

</main-mask>

<!-- 调货入库弹窗 -->
<main-mask :maskStatus="isShowMaskJh" :mWidth="1500" :mHeight="900"  @onClose="onCloseDJh">
  <template v-slot:content>
    <view class="mask_title">调货入库</view>
    <view class="tables">
      <view class="thead">
        <view class="tr">
          <view class="td">商品</view>
          <view class="td">进货量</view>
          <view class="td">门店</view>
        </view>
      </view>
      <view class="tbody">
        <scroll-view scroll-y="true" style="height:500rpx">
      <view class="tr"  v-for="(list,index) in jhlist" :key="index">
        <view class="td">{{list.goodsname}}</view>
        <view class="td">{{list.num}}</view>
        <view class="td">{{list.mdname}}</view>
      </view>	
    </scroll-view>
      </view>
    </view>
    <view class="dhd_bottom"> 
      <button>确认</button>
      <button @click="onParentColseJh">取消</button>
    </view>
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
		 current: 0,//选中状态
		 isShowMask:false,//商品入库弹出层状态，
     mWidth:1000,
     mHeight:800,
		 isShowMaskDhd:false,//商品入库弹出层状态，		
     isShowMaskJh:false,//调货入库弹出层状态，
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
      // 订货单
      dhdlist:[
              {id: '458',num:'1', goodsname: '波士顿大龙虾',unit: "斤",sjnum: 1.,lastprice:0,lastnum:0,remark:"鱼 2斤" },
              {id: '458',num:'1',  goodsname: '波士顿大龙虾',unit: "斤",sjnum: 1.01,lastprice:0,lastnum:0,remark:"鱼 2斤" },
              {id: '458',num:'1',  goodsname: '波士顿大龙虾',unit: "斤",sjnum: 1.01,lastprice:0,lastnum:0,remark:"鱼 2斤" },
              {id: '458',num:'1',  goodsname: '波士顿大龙虾',unit: "斤",sjnum: 1.01,lastprice:0,lastnum:0,remark:"鱼 2斤" },
              {id: '458',num:'1',  goodsname: '波士顿大龙虾',unit: "斤",sjnum: 1.01,lastprice:0,lastnum:0,remark:"鱼 2斤" },
              {id: '458',num:'1',  goodsname: '波士顿大龙虾',unit: "斤",sjnum: 1.01,lastprice:0,lastnum:0,remark:"鱼 2斤" },
              {id: '458',num:'1',  goodsname: '波士顿大龙虾',unit: "斤",sjnum: 1.01,lastprice:0,lastnum:0,remark:"鱼 2斤" },
              {id: '458',num:'1',  goodsname: '波士顿大龙虾',unit: "斤",sjnum: 1.01,lastprice:0,lastnum:0,remark:"鱼 2斤" },
              {id: '458',num:'1',  goodsname: '波士顿大龙虾',unit: "斤",sjnum: 1.01,lastprice:0,lastnum:0,remark:"鱼 2斤" },
			],
      // 调货入库
      jhlist:[
              {id: '458',num:'1', goodsname: '波士顿大龙虾',mdname: "总店", },
              {id: '458',num:'1', goodsname: '波士顿大龙虾',mdname: "总店", },
              {id: '458',num:'1', goodsname: '波士顿大龙虾',mdname: "总店", },
              {id: '458',num:'1', goodsname: '波士顿大龙虾',mdname: "总店", },
              {id: '458',num:'1', goodsname: '波士顿大龙虾',mdname: "总店", },
              {id: '458',num:'1', goodsname: '波士顿大龙虾',mdname: "总店", },

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
		//打开商品入库弹出层
		onShowMask(){
			this.isShowMask = true
		},
		// 关闭商品入库弹出层
		onClose(e){
			this.isShowMask = e
		},
    // 点击订货单入库
    onDhd(){
			this.isShowMaskDhd = true
    },
    //取消订货单
    onParentColseDhd(){
			this.isShowMaskDhd = false
    },
    // 关闭订货单入库弹窗 子组件传过来
    onCloseDhd(e){
			this.isShowMaskDhd = e
    },
    
    // 点击调货入库
    onJh(){
			this.isShowMaskJh = true
    },
    //取消调货入库
    onParentColseJh(){
			this.isShowMaskJh = false
    },
    // 关闭调货入库弹窗 子组件传过来
    onCloseDJh(e){
			this.isShowMaskJh = e
    },
    goLink(){
      // console.log(123);
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
.onsubmit button{
	background-color: #009688;
	color: #fff;
	margin: 20rpx 100rpx;

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
