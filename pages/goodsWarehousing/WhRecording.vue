<template>
  <view class="WhRecording">

    <view class="rec_head">
        <text class="rec_head_1">操作时间选择</text>
        <text >   
        <picker mode="date" :value="date" :start="startDate" :end="endDate" @change="bindDateChange">
        <view class="uni-input">{{date}}</view>
      </picker>
    </text>
    <button class="export">导出纪录</button>
  </view>



  </view>
</template>

<script>
export default {
  name: "WhRecording",
  components: {},
  props: {},
  data() {
    const currentDate = this.getDate({
            format: true
        })
    return {
      date: currentDate,
    }
  },
  computed: {
    startDate() {
            return this.getDate('start');
        },
        endDate() {
            return this.getDate('end');
        }
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
  watch: {},

  // 页面周期函数--监听页面加载
  onLoad() {},
  // 页面周期函数--监听页面初次渲染完成
  onReady() {},
  // 页面周期函数--监听页面显示(not-nvue)
  onShow() {},
  // 页面周期函数--监听页面隐藏
  onHide() {},
  // 页面周期函数--监听页面卸载
  onUnload() {},
  // 页面处理函数--监听用户下拉动作
  // onPullDownRefresh() { uni.stopPullDownRefresh(); },
  // 页面处理函数--监听用户上拉触底
  // onReachBottom() {},
  // 页面处理函数--监听页面滚动(not-nvue)
  // onPageScroll(event) {},
  // 页面处理函数--用户点击右上角分享
  // onShareAppMessage(options) {},
} 
</script>

<style scoped>
.rec_head{ 
  display: flex;
  align-items: center;
}
.export{
  margin-left: 20rpx;
}
.rec_head_1{

}
</style>