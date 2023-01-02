<template>
	<view class="collection">
		<!-- 返回主菜单按钮 -->
		<main_menu></main_menu>
		<view class="top_cell">
			
			<view class="search_box">
				<input placeholder="请输入商品名称或首字母">
			</view>
			
		</view>

	</view>
</template>

<script>
import main_menu from '../components/Main_menu/Main_menu.vue';

export default {
	components: {
		main_menu,
	
	},
	data() {
		return {
			
		
		}
	},
	methods: {
		
	}
}
</script>

<style scoped>
.top_cell {
	padding: 40rpx 20rpx;
	background-color: #e6e6e6;
	display: flex;
	justify-content: center;
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




</style>
