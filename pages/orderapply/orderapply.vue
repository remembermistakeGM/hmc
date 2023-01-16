<template>

	<view class="orderapply">

      <view class="orderapply-list-cell">
				<view class="orderapply-list-cell-left">
					当前选择
				</view>
                <picker  mode="date" :value="date" :start="startDate" :end="endDate" @change="bindDateChange">
                    <view class="orderapply-date">{{date}}</view>
                </picker>
                    <button>搜索</button>
			</view>
      <view class="tables">
		<view class="thead">
			<view class="tr">
				<view class="td">序号</view>
				<view class="td">门店</view>
				<view class="td">进货时间</view>
				<view class="td">商品</view>
				<view class="td">进货量</view>
				<view class="td">单位</view>
				<view class="td">实际进货量</view>
				<view class="td">录入采购价</view>
				<view class="td">备注</view>
			</view>
		</view> 
		<view class="tbody">
		<view class="tr"  v-for="(item,index) in list" :key="index">
			<view class="td">{{item.id}}</view>
			<view class="td">{{item.jhtime}}</view>
			<view class="td">{{item.jhtime}}</view>
			<view class="td">{{item.goodsname}}</view>
			<view class="td">{{item.jhnum}}</view>
			<view class="td">{{item.unit}}</view>
			<view class="td">{{item.sjnum}}</view>
			<view class="td">{{item.cjprice}}</view>
			<view class="td">{{item.bz}}</view>
		</view>	
		
		</view>

	</view>


            
	</view>

</template>

<script>


	export default {
    data() {
          const currentDate = this.getDate({
            format: true
        })
        return {
            list:[
                {id:12,mdname:'你好技',jhtime:"2021-20-10",goodsname:"鱼",jhnum:12,unit:"斤",sjnum:12,cjprice:12,bz:"㔿"},
                {id:12,mdname:'你好技',jhtime:"2021-20-10",goodsname:"鱼",jhnum:12,unit:"斤",sjnum:12,cjprice:12,bz:"㔿"},
                {id:12,mdname:'你好技',jhtime:"2021-20-10",goodsname:"鱼",jhnum:12,unit:"斤",sjnum:12,cjprice:12,bz:"㔿"},
                {id:12,mdname:'你好技',jhtime:"2021-20-10",goodsname:"鱼",jhnum:12,unit:"斤",sjnum:12,cjprice:12,bz:"㔿"},

            ],
             date: currentDate,
        };
    },
      computed: {
        startDate() {
            return this.getDate('start');
        },
        endDate() {
            return this.getDate('end');
        }
    },
    onLoad() {
    },
    methods: {
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
        }
    },
    components: {  

    }
}
</script>

<style scoped>
.orderapply-list-cell{
    display: flex;
    align-items: center;
    padding:20rpx;
}
.orderapply-list-cell .orderapply-list-cell-left{
color: #666;
}
.orderapply-date{
    margin: 0rpx 15rpx;
    border: 1rpx solid #ccc;
    padding: 10rpx;
    border-radius: 6rpx;
    color: #666;
}
.orderapply-list-cell button{
    margin-left: 60rpx;
    background:#009688;
    color: #fff;
    line-height: 1.7rem;
    height: 1.7rem;
    font-size: 0.9rem;
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
 
</style>
