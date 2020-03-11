<template>
	<view class="content">
		<view  class="advance-area">
			<view class="flex-box tc thead">
				<view class="item-3">产品种类</view>
				<view class="item-3">送检样品量(克)</view>
			</view>
			<view class="flex-box table tc">
				<view class="item-3">
					水产品
				</view>
				<view class="item-3">
					<view class="table-flex">
						<view class="item">鱼类≥100g(如一整条不足100g,需送检多条以达到送检量);虾贝类≥2500g</view>
					</view>
				</view>
			</view>
			<view class="flex-box table tc">
				<view class="item-3">
					蔬菜瓜果
				</view>
				<view class="item-3">
					<view class="table-flex">
						<view class="item">
							送检样≥100g,整个或整颗,至少一个且重量≥100g
						</view>
					</view>
				</view>			
			</view>
			<view class="flex-box table tc">

				<view class="item-3">
					<view class="table-flex">
						<view class="item">禽畜类</view>
						<view class="item">蛋类</view>
						<view class="item">香肠、熏肉、盐渍水产品、酱腌菜等</view>
						<view class="item">米粉、豆制品</view>
						<view class="item">食用菌、银耳、黄花菜、菜干等</view>
						<view class="item">牛百叶、海蜇、牛筋、海参等</view>
						<view class="item">肉馅等</view>
					</view>
				</view>
				<view class="item-3">
					送样量≥100g
				</view>

			</view>
		</view>
				 <button type="warn" size = "mini" @click="back" >关闭</button>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods:{
			back() {
				uni.navigateBack({
					url:'addSample'
				})
			}
		}
	}
</script>

<style lang="scss">
	$color:#e0e0e0;
	.content {
		display: flex;
		flex: 1;
		flex-direction: column;
		background-color: #fbf9fe;
	}
	
	.flex-box {
		display: flex;
		flex-wrap: wrap;
	}
	
	
	.flex-box>.item-2 {
		flex: 0 0 50%;
	}
	
	.flex-box>.item-3 {
		flex: 0 0 50%;
	}
	
	.title{
		margin: 20upx 0;
		color: red;
	}
	
	//普通表格
	.genaral-area {
		.item-2 {
			font-size: 26upx;
			border: 1upx solid $color;
			border-width: 1upx 1upx 0 0;
			padding: 16upx 0;
			box-sizing: border-box;
			text-align: center;
	
			&:first-child {
				border-left-width: 1upx;
			}
	
			&:last-child {
				border-right-width: 1upx;
			}
		}
	
		.thead {
			.item-2 {
				font-weight: bold;
	
				box-sizing: border-box;
			}
		}
	
		.table {
			&:last-child {
				border-bottom: 1upx solid $color;
			}
	
			.item-2 {
				display: flex;
				justify-content: center;
				align-items: center;
				box-sizing: border-box;
			}
		}
	}
	
	
	// 多行合并表格
	.advance-area {
		.item-3 {
			font-size: 26upx;
			border: 1upx solid $color;
			border-width: 1upx 1upx 0 0;
			box-sizing: border-box;
			text-align: center;
	
			&:first-child {
				border-left-width: 1upx;
			}
	
			&:last-child {
				border-right-width: 1upx;
			}
		}
	
		.thead {
			.item-3 {
				font-weight: bold;
				padding: 16upx 0;
				box-sizing: border-box;
			}
		}
	
		.table {
			&:last-child {
				border-bottom: 1upx solid $color;
			}
	
			.item-3 {
				display: flex;
				justify-content: center;
				align-items: center;
				box-sizing: border-box;
			}
		}
	
		.table-flex {
			flex: 1;
	
			.item {
				border-bottom: 1upx solid $color;
				padding: 10upx 0;
				box-sizing: border-box;
	
				&:last-child {
					border-width: 0;
				}
			}
		}
	}
</style>
