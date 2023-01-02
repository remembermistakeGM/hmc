<template>
	<!-- 分类 -->
    <view class="claassify_group">
        <view class="classify_item" v-for="(item, index) in classify" :key="index"
            :class="[item.isSelect == '1' ? 'is_active' : '']"><text>
                {{ item.title }}
            </text>
        </view>
    </view>
</template>

<script>
	export default {
		data() {
			return {
				classify: [
                    { title: "全部", isSelect: 1 },
                    { title: "蟹类", isSelect: 0 },
			],
			}
		},
		methods: {
		
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
