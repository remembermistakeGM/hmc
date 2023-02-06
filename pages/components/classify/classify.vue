<template>
	<!-- 分类 -->
    <view class="claassify_group">
        <view  class="classify_item" v-for="(item, index) in classifylist" :key="index"
             :class="[ifyCurrent == index ? 'is_active' : '']" @click="onClassify" :data-index="index"><text>
                {{ item.title }}
            </text> 
        </view>
    </view>
</template>

<script>
	export default {
		props: {
   		 classifylist:{
     	 type:Array,
     	 default:[]
		},
		},
		data() {
			return {
				ifyCurrent:0
			}
		},
		methods: {
			onClassify(e){
				const i = e.currentTarget.dataset.index
				this.ifyCurrent = i
			}
		}
	}
</script>
<style>
.claassify_group {
	display: flex;
	flex-wrap: wrap;
	margin: 40rpx;
    padding-left: 100rpx;
}
.claassify_group .classify_item {
	border: 1rpx solid #eee;
	margin-left: 20rpx;
	padding: 0rpx 40rpx;
	line-height: 3rem;
	height: 3rem;
	font-size: 1.2rem;
	color: #666;
	margin-top: 20rpx;
}

.is_active {
	color: #21ad42 !important;
	border-color: #21ad42 !important;
}
</style>
