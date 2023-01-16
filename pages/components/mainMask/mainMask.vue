<template>
  <!-- 弹出层 -->
  <view class="mask—center" v-if="maskStatus" >
    <!-- 可设置宽高 默认1000 ，800 -->
    <view class="mask_main" :style="{width:mWidth+'rpx',height:mHeight+'rpx'}"  :class="{'modal': 'maskStatus'}">
      <slot name="content"></slot>
    </view> 
  <view class="mask_bg"  @click="onClose"></view>
  </view>

</template>

<script>
export default {
  name: "mainMask",
  components: {},
  props: {
    maskStatus:{
      type:Boolean,
      default:false
    },
    mWidth:{
      type:Number,
      default:1000
    },
    mHeight:{
      type:Number,
      default:800
    },
  },
  data() {
    return {  
      
    }
  },
  computed: {},
  methods: {

    onClose(){
      this.$emit('onClose',false)
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

} 
</script>
<style scoped>
.mask_main{
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 1000rpx;
  height: 1000rpx;
  z-index: 9999;
  background-color: #fff;
  border-radius: 18rpx;
	padding: 20rpx;
  overflow: hidden;
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
@keyframes scaleUp {
	0% {
	  transform: scale(0.8)  translateY(500px) translateX(-50%)  translateY(-50%);
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
</style>