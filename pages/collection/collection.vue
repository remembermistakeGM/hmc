<template>
	<view class="collection">
		<view class="top_cell">
			
			<view class="search_box">
				<input placeholder="请输入商品名称或首字母">
			</view>
			
		</view>
		<view class='coll_content'>
			<!-- 左边 -->
			<view class='dk_goods_list'>
				<view class='dk_group'>
					<view class='dk_cell'>
						<view class='dk_cell_md3'>商品</view>
						<view class='dk_cell_md3'>数量(重量)</view>
						<view class='dk_cell_md3'>操作</view>
					</view>
				<scroll-view scroll-y="true" style="height: 460px;">
					<view v-for="(item ,index) in coll" class='dk_list' :class="[currentCart==index ? 'cartactive':'']" :key="index" :data-index="index" @click="onSelectcart">
					<view class='dk_list_md3'>{{item.name}}</view>
						<view class='dk_list_md3'>
							<input class="dk_list_input"  placeholder="0" v-model="item.num"   @input="onChange" />
							<text class="dk_list_price">单价:{{item.price}}</text>
							<text class="dk_list_total">小计:12</text>
						</view>
						<view class='dk_list_md3'><text class="iconfont icon-shanchu"></text></view>
					
					</view> 
				</scroll-view> 
				<view class='btnsbox'>
					<text>立即收银</text>
					<text>￥3.3</text>
				</view>
				</view>
			</view>

			<!-- 右边 -->
			<view class='classify_list'>
				<view class='classify_group'>
					<view class='classify_cell' >
					
						<view v-for="(item,index) in cate" 
							class='changecate' 
							:class="[current==index ? 'cateactive':'']"
							:key="index" 
							@click="changecate"
							:data-index="index"
							>{{item.name}}</view>
					</view>
				</view>
				<view class='classify_content'>
				<scroll-view scroll-y="true" style="height:450px">
					<view class='classify_group_md4'>
					<view class='classify_md4' v-for="(item ,index) in goodsList" :key="index" >
						<view class='classify_grid_demo' @click="onSelect" :data-index="index" :data-idx="item.id" >
							<view class='goodsimg' ><image :src="item.src"></image></view>
							<view class='goodsinfo'>
								<text class="name">{{item.name}}</text>
								<text class="unit">单位:{{item.unit}}</text>
								<text class="price">￥{{item.price}}</text>
							</view>
						</view>
					</view>
				</view>
				</scroll-view>
				</view>
			</view>

		</view>
	</view>
</template>

<script>

export default {
	components: {
	
	},
	data() {
		return {
			coll:[],
			cate:[
				{id:1,name:"虾类"},
				{id:1,name:"虾类"},
				{id:1,name:"虾类"},
				{id:1,name:"虾类"},
				{id:1,name:"虾类"},
				{id:1,name:"虾类"},
				{id:1,name:"虾类"},
				{id:1,name:"虾类"},
				{id:1,name:"虾类"},
				{id:1,name:"虾类"},
				{id:1,name:"虾类"},
				{id:1,name:"虾类1"},
			],
			current:0,
			goodsList:[
				{id:1,name:"标品",src:"https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-08-10/62f3089adb43b.jpg",unit:"斤",price:"10",num:0,idbp:1},
				{id:12,name:"非标品",src:"https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-08-10/62f3089adb43b.jpg",unit:"斤",price:"20",num:0,idbp:0},
				{id:13,name:"标品",src:"https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-08-10/62f3089adb43b.jpg",unit:"斤",price:"30",num:0,idbp:1},
				{id:10,name:"非标品",src:"https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-08-10/62f3089adb43b.jpg",unit:"斤",price:"10",num:0,idbp:0},
				{id:11,name:"王牌",src:"https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-08-10/62f3089adb43b.jpg",unit:"斤",price:"10",num:0,idbp:1},
				{id:18,name:"王牌",src:"https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-08-10/62f3089adb43b.jpg",unit:"斤",price:"10",num:0,idbp:1},
				{id:15,name:"王牌",src:"https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-08-10/62f3089adb43b.jpg",unit:"斤",price:"10",num:0,idbp:1},
				{id:16,name:"王牌",src:"https://swjls.shuxiaoliu.com//Uploads/image/goods/2022-08-10/62f3089adb43b.jpg",unit:"斤",price:"10",num:0,idbp:1},
			],
			currentCart:0
		}
	},
	methods: {
		changecate(e){
			this.current = e.currentTarget.dataset.index
		},
		onSelect(e){
			const i = e.currentTarget.dataset.idx //商品id
			const index = e.currentTarget.dataset.index //商品索引
			let coll =this.coll //购物车
			let  goodsList = this.goodsList //显示商品列表
			let newColl=[] 
			// this.currentCart = e.currentTarget.dataset.index //选中
			// 标品
			if(goodsList[index].idbp){ //是否是标品  标品再次点击+1
		 	if(coll.length!==0){//判断数组是否有商品  有商品才能判断
				let arr = coll.filter((item,index) => { //返回符合条件的数组，购物车是否存在此商品
					// let cartIndex=index
		           return i == item.id;
		          });
			   
				
				 if(arr.length!==0){ //购物车已经存在商品，再次点击数量+1
					 arr[0].num+=1
				
					 let cartindex= coll.findIndex((item) =>{//返回符合条件的数组索引，并添加选中状态
					 return i == item.id
					}) 
					this.currentCart=cartindex
	
					
				 }else{ //购物车不存在商品，加入购物车
					newColl=goodsList[index]
					newColl.num=1
					this.coll.push(newColl)

					let cartindex= coll.findIndex((item) =>{//返回符合条件的数组索引，并添加选中状态
					 return i == item.id
					}) 
					this.currentCart=cartindex

				 }
			  }else{// 没有商品 添加一个商品，加入购物车
				newColl=goodsList[index]
				newColl.num=1
				this.coll.push(newColl)
			
				let cartindex= coll.findIndex((item) =>{//返回符合条件的数组索引，并添加选中状态
					 return i == item.id
					}) 
					this.currentCart=cartindex
			}
			//非标品
		    }else{ 
			 if(coll.length!==0){//判断数组是否有商品  有商品才能判断
				let arr1 = coll.filter((item,index) => {//返回符合条件的数组，购物车是否存在此商品
		          return i == item.id;
		         });
				 
				 if(arr1.length!==0){//购物车已经存在商品，再次点击没用

					let cartindex= coll.findIndex((item) =>{//返回符合条件的数组索引，并添加选中状态
					 return i == item.id
					}) 
					this.currentCart=cartindex

					 return false;
				 }else{//购物车不存在商品，加入购物车
					newColl=goodsList[index]
					this.coll.push(newColl)

					let cartindex= coll.findIndex((item) =>{//返回符合条件的数组索引，并添加选中状态
					 return i == item.id
					}) 
					this.currentCart=cartindex
				 }
			}else{// 没有商品 添加一个商品，加入购物车
				newColl=goodsList[index]
				this.coll.push(newColl)

				let cartindex= coll.findIndex((item) =>{//返回符合条件的数组索引，并添加选中状态
					 return i == item.id
					}) 
					this.currentCart=cartindex

			}

		 }

			
		},
		onSelectcart(e){
			this.currentCart = e.currentTarget.dataset.index
		}
		// onChange(e){
		// 	const { value } = e.target;
		// 	console.log("检测到变化"+value);
		// }

	},
	
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
.coll_content{
	display: flex;
}
.dk_goods_list{
	box-sizing: border-box;
	border: 1px solid rgb(241, 241, 241);
	height: 580px;
	width: 25%;
	position: relative;
}
.classify_list{
	box-sizing: border-box;
	border: 1px solid rgb(241, 241, 241);
	width: 75%;
	height: 580px;

}
.dk_cell{
	display: flex;
	border-bottom: 1px solid #e5e5e5;
	padding: 20rpx 5rpx;
	font-size: 1rem;
	color: #000;
	font-weight: bold;
	box-sizing: border-box;
}

.dk_cell_md3{
	flex: 1;
	text-align: center;
}
.dk_list{
	display: flex;
	border-bottom: 1px solid #e5e5e5;
	padding: 20rpx 0rpx;
	font-size: 0.8rem;
	color: rgb(92, 92, 92);
	box-sizing: border-box;
}
.cartactive{
	background-color: rgb(241, 241, 241);
}
.cartactive input{
	border-color:#ff0000 !important; 
}
.dk_list_md3{
	flex: 1;
	text-align: center;
}
.dk_list_md3 .dk_list_input{
	width: 80px;
	box-sizing: border-box;
	margin: 0px auto;
	border: 1rpx solid #eee;
	text-align: center;
	line-height: 1.6rem;
	color: #000;
}
.dk_list_md3 .dk_list_price{
	display: block;
	margin: 4rpx 0;
	font-size: 0.75rem;
}
.dk_list_md3 .dk_list_total{
	font-size: 0.75rem;
	color: #ff0000;
}
.btnsbox{
position: absolute;
width: 100%;
height: 70px;
bottom: 0px;
color: #fff;
background-color: #ff9800;
font-weight: bold;
text-align: center;
font-size: 1rem;
}

.btnsbox text{
	display: block;
	text-align: center;
	padding-top: 10rpx;
}
.classify_group{
	padding: 10px;
}
.classify_cell{
	overflow-x:auto;overflow-y:hidden;white-space:nowrap;
	width: 100%;
}
.changecate{
display: inline-block;
padding: 0px 25px;
margin: 0px 10px;
line-height: 35px;
font-size: 16px;
color: #666;
border: 1px solid #eee;
transition: all .3s ease;
}
.changecate.cateactive{
color: #21ad42;
border: 1px solid #21ad42;
}
.classify_content{
	
}
.classify_group_md4{
	display: flex;
	flex-wrap: wrap;
}
.classify_md4{
	width: 25%;
	
}
.classify_grid_demo{
	box-sizing: border-box;
	height: 100px;
	margin: 5px;
	border: 2px solid #009688;
	display: flex;
}
.classify_grid_demo .goodsimg{
width: 30%;
height:100%;
}
.classify_grid_demo .goodsimg image{
width: 100%;
height:100%;
overflow: hidden;
display: block;
}
.goodsinfo{
padding: 6rpx 10rpx;
}
.goodsinfo {
	font-size: 0.8rem;
}
.goodsinfo .name{
	font-size: 0.85rem;
}
.goodsinfo .unit{
	margin:16rpx 0;
	display: block;
	color: #666;
}
.goodsinfo .price{
	font-weight: bold;
}
</style>
