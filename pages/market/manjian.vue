<template>
  <view class="manjian">
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
		<view class="mj_cell_text">优惠项{{index+1}}</view>
		<view class="mj_cell_input">
			<input type="text" :value="item.num1" placeholder="0" />
			<text>元，减</text>
			<input type="text" :value="item.num2" placeholder="0" />
			<text>元</text>
		</view>	
	</view>

		<view class="mj_cell">
			<button class="mj_cell_btn"  @click="plus">+添加优惠项</button>
			<button class="mj_cell_btn" @click="reduce">-删除优惠项</button>
	</view>
  </view>
</template>

<script>
export default {
  data() {
	  const currentDate = this.getDate({
            format: true
		})
		 const currentDate1 = this.getDate({
            format: true
        })
    return {
      items: [
        { value: "1", name: "开启" },
        { value: "0", name: "关闭", checked: "true" }
      ],
	  current: 0,
	 date: currentDate,
	 date1: currentDate1,
		yhList:[
			
		]

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
	 
		let obj={
			id:"1",
			num1:"",
			num2:""
		}
	  this.yhList.push(obj);
	 console.log(this.yhList)
  },
     reduce:function(){
	
	 this.yhList.shift();
	 console.log(this.yhList)
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
</style>
