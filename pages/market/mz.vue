<template>
  <view class="mz">
    <view class="mj_cell">
      <view class="mj_cell_text">是否开启</view>
	  <view class="mj_cell_label">
      <radio-group @change="radioChange" class="mj_cell_radio">
        <label
          class="uni-list-cell uni-list-cell-pd"
          v-for="(item, index) in items"
          :key="item.value"
        >
          <view>
            <radio :value="item.value" :checked="index === current"/>
          </view> 
          <view>{{item.name}}</view>
        </label>
      </radio-group>
</view>
    </view>
	<view v-if="!current">
    <view class="mj_cell">
      <view class="mj_cell_text">活动时间</view>
	  <view class="mj_cell_label">
	  	<picker mode="date" :value="date" :start="startDate" :end="endDate" @change="bindDateChange">
			<view class="uni-input">{{date}}</view>
		</picker>
		<text>一</text>	
		<picker mode="date" :value="date1" :start1="startDate1" :end1="endDate1" @change="bindDateChange1">
			<view class="uni-input">{{date1}}</view>
		</picker>
   </view>
    </view> 

	<view class="mj_cell yh" v-for="(item,index) in yhList" :key="index"> 
		<view class="mj_cell_text">购买商品：</view>
		<view class="mj_cell_input">
			<view class='tj_goods' @click="onSelectGoods1(index)">
				<text v-if="item.goods1_id">{{item.goods1_name}} ￥{{item.goods1_price}}</text>
				<text v-else>选择商品</text>
			</view>

			<text class="texttj">赠送商品</text>
			<view class='tj_goods' @click="onSelectGoods2(index)"> 
				<text v-if="item.goods2_id">{{item.goods2_name}} ￥{{item.goods2_price}}</text>
				<text v-else>选择商品</text>
			</view>
		
		</view>	
		<view class='closebtn'><image @click="reduce" :data-index="index" src="../../static/close-circle.svg"></image></view>
	</view>
		<view class="mj_cell">
			<button class="mj_cell_btn"  @click="plus">添加买赠商品</button>
	</view>
</view>
	<!-- 选择商品弹窗 -->
<main-mask :maskStatus="isShowMask"  :mWidth="1500" :mHeight="900"  @onClose="onCloseMask">
	<template v-slot:content> 
	  <view class="mask_title">选择买赠商品</view>
	  <view class='searchbox'><input type="text" placeholder="请输入商品名称"><button>搜索</button></view>
	  <view class="tables">
		<view class="thead">
		  <view class="tr">
			<view class="td">商品</view>
			<view class="td">价格</view>
			<view class="td">操作</view>
		  </view>
		</view>
		<view class="tbody">
		  <scroll-view scroll-y="true" style="height:500rpx">
		<view class="tr"  v-for="(list,index) in goodslist" :key="index">
		  <view class="td">{{list.goodsname}}</view>
		  <view class="td">￥{{list.price}}</view>
		  <view class="td"><button @click="onSelectgoods" class="goodsbtn" :data-idx="index">选择</button></view>
		</view>	
	  </scroll-view>
		</view>
	  </view>
	  <view class="dhd_bottom"> 
		
		<button @click="onParentColse">关闭</button>
	  </view>
	</template>
  
  </main-mask>
  </view>
  
</template>

<script>
import mainMask from '../components/mainMask/mainMask.vue';
export default {
	components:{
		mainMask
	},
  data() {
	   const currentDate = this.getDate({
            format: true
		})
		 const currentDate1 = this.getDate({
            format: true
        })
    return {
      items: [
        { value: "1", name: "开启",  },
        { value: "0", name: "关闭",checked: "true" }
      ],
	  current: 1,
	 date: currentDate,
	 date1: currentDate1,
		yhList:[
			
		],
		isShowMask:false,
			// 
			goodslist:[
              {id: '458',price:'1', goodsname: '波士顿大龙虾', },
              {id: '458',price:'10', goodsname: '波士顿大龙虾', },
              {id: '458',price:'01', goodsname: '波士顿大龙虾', },
              {id: '458',price:'122', goodsname: '波士顿大龙虾', },
              {id: '458',price:'123', goodsname: '波士顿大龙虾', },
              {id: '458',price:'1', goodsname: '波士顿大龙虾', },
              {id: '458',price:'1', goodsname: '波士顿大龙虾', },
              {id: '458',price:'1', goodsname: '波士顿大龙虾', },
			],
			goods_index:-1,//列表索引
			goods1_index:0,//判断第一个商品还是第二个商品
		


    };
  },
computed: {
	startDate() {
		return this.getDate('start');
	},
	endDate() {
		return this.getDate('end');
	},
	startDate1() {
		return this.getDate('start1');
	},
	endDate1() {
		return this.getDate('end1');
	}
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
	bindDateChange: function(e) {
            this.date = e.detail.value
		},
		getDate(type) {
            const date = new Date(); 
            let year = date.getFullYear();
            let month = date.getMonth() + 1;
            let day = date.getDate();
            if (type === 'start') {
                year = year - 60;
            } else if (type === 'end') {
                year = year + 2;
            }
            month = month > 9 ? month : '0' + month;
            day = day > 9 ? day : '0' + day;
            return `${year}-${month}-${day}`;
		},
		bindDateChange1: function(e) {
            this.date1 = e.detail.value
		}, 
	
   plus:function(){
	// this.isShowMask=true
	 let obj={
		id:0,
		goods1_id:"",
		goods1_name:"",
		goods1_price:"",
		goods2_id:"",
		goods2_name:"",
		goods2_price:"",
	}
	this.yhList.push(obj)
  },
     reduce:function(e){ 
		const index = e.currentTarget.dataset.index
		this.yhList.splice(index,1)
  },
  onCloseMask(e){
	this.isShowMask=e
  },
  onSelectgoods(e){
	const index = e.currentTarget.dataset.idx //商品列表的索引
	const id1 = this.goods1_index //判断是第一个还是第二个
	let id =this.goods_index //索引
	const goodslist = this.goodslist //商品列表
	if(id1==1){ //第一个商品
		this.yhList[id].goods1_id=goodslist[index].id
		this.yhList[id].goods1_price=goodslist[index].price
		this.yhList[id].goods1_name=goodslist[index].goodsname
	}

	if(id1==2){ //第二个商品
		this.yhList[id].goods2_id=goodslist[index].id
		this.yhList[id].goods2_price=goodslist[index].price
		this.yhList[id].goods2_name=goodslist[index].goodsname
	}
	this.isShowMask=false
  },
  onParentColse(){
	this.isShowMask=false
 },
 onSelectGoods1(e){
	this.goods_index = e
	this.goods1_index = 1
	this.isShowMask=true
 },
 onSelectGoods2(e){
	this.goods_index = e
	this.goods1_index = 2
	this.isShowMask=true
 }
 
 },


   
};
</script>

<style scoped>
.mj_cell{
	display: flex;
	padding:40rpx 40rpx;
	align-items: center;
	margin-left: 80rpx;
}
.mj_cell_text{
	font-size: 0.9rem;
}

.uni-list-cell{
	display: flex;
	padding-left: 30rpx;
	font-size: 0.89rem;
	align-items: center;
}
.mj_cell_radio{
	display: flex;
}
.mj_cell_label{
	display: flex;
	font-size: 0.89rem;
	align-items: center;
}
.mj_cell_label .uni-input{
	padding: 10rpx 10rpx;
	background-color: #f2f2f2;
	border-radius: 6rpx;
	margin: 0rpx 10rpx;

}
.mj_cell_input{
	display: flex;
	font-size: 0.89rem;
	align-items: center;
}
.mj_cell_input input{
	border: 1px solid #ccc;
	margin: 0rpx 10rpx;
	padding: 6rpx;
	border-radius: 4rpx;
	text-align: center;
}
.mj_cell_btn{
	width:250rpx;
	margin: 0rpx 10rpx;
	font-size: 0.8rem;
	}
.mj_cell_btn:nth-child(1){
	background-color: rgb(15, 28, 52);
	color: #fff;
}
.texttj{
	padding: 0rpx 20rpx;
}
.tj_goods{
	font-weight: bold;
	padding: 8rpx;
	background: #ccc;
}
.closebtn image{
	width:60rpx;
	height: 60rpx;
	margin-left: 60rpx;
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
  padding: 20rpx;
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
.mask_title{
	font-weight: bold;
	text-align: center;
	margin: 30rpx auto;
}
.goodsbtn{
	background-color: #009688;
	color: #fff;
	width: 108rpx;
	font-size: 0.6rem;

}
.searchbox{
	display: flex;
	align-items: center;
	justify-content: center;
	margin-bottom: 20rpx;

}
.searchbox input{
	width: 600rpx;
	padding: 8rpx;
	height: 1.6rem;
	background-color: #d6d6d6;
}
.searchbox button{
	width:120rpx;
	background-color: #009688;
	color: #fff;
	font-size: 0.8rem;
	margin: 10rpx;
}
</style>
