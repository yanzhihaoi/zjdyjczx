<template>
<view class="content">
	   <view style="text-align: center;">广东中检达元检测技术有限公司 \n</view>
	   <view style="text-align: center;">快检检测报告 \n</view>
		<view  class="advance-area">
			<view class="flex-box tc thead">
				<view class="item-3-1">序号</view>
				<view class="item-3-2">样品名称</view>
				<view class="item-3-3">检测项目</view>
				<view class="item-3-4">快检结果</view>
				<view class="item-3-5">检测标准</view>
			</view>

			<view class="flex-box table tc">
				<view class="item-3-1">
					<view class="table-flex">
						<view class="item">1</view>
						<view class="item">2</view>
						<view class="item">3</view>
						<view class="item">4</view>
						<view class="item">5</view>
						<view class="item">6</view>
						<view class="item">7</view>
					</view>
				</view>
				
				<view class="item-3-2">
					<view class="table-flex">
						<view class="item">西瓜子</view>
						<view class="item">红樱桃</view>
						<view class="item">3</view>
						<view class="item">4</view>
						<view class="item">5</view>
						<view class="item">6</view>
						<view class="item">7</view>
					</view>
				</view>
				
				<view class="item-3-3">
					<view class="table-flex">
						<view class="item">二氧化碳</view>
						<view class="item">有机磷和氨基甲酸脂类农药残留</view>
						<view class="item">3</view>
						<view class="item">4</view>
						<view class="item">5</view>
						<view class="item">6</view>
						<view class="item">7</view>
					</view>
				</view>
				
				<view class="item-3-4">
					<view class="table-flex">
						<view class="item">GB 2760-2014</view>
						<view class="item">GB 2760-2014</view>
						<view class="item">3</view>
						<view class="item">4</view>
						<view class="item">5</view>
						<view class="item">6</view>
						<view class="item">7</view>
					</view>
				</view>
				<view class="item-3-5">
					<view class="table-flex">
						<view class="item">合格</view>
						<view class="item">合格</view>
						<view class="item">3</view>
						<view class="item">4</view>
						<view class="item">5</view>
						<view class="item">6</view>
						<view class="item">7</view>
					</view>
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
				
			}
		},
		methods: {
			back(){
				uni.navigateBack({
					url:'orderDetails'
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
		flex: 0 0 20%;
	}
	.flex-box>.item-3-1 {
		flex: 0 0 10%;
	}
	.flex-box>.item-3-2 {
		flex: 0 0 20%;
	}	
	.flex-box>.item-3-3 {
		flex: 0 0 30%;
	}
	.flex-box>.item-3-4 {
		flex: 0 0 22%;
	}
	.flex-box>.item-3-5 {
		flex: 0 0 18%;
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
		.item-3 ,.item-3-1 ,.item-3-2 ,.item-3-3, .item-3-4, .item-3-5, .item-3-6 {
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
			.item-3 ,.item-3-1 ,.item-3-2 ,.item-3-3, .item-3-4, .item-3-5, .item-3-6 {
				font-weight: bold;
				padding: 16upx 0;
				box-sizing: border-box;
			}
		}
	
		.table {
			&:last-child {
				border-bottom: 1upx solid $color;
			}
	
			.item-3 .item-3-1 .item-3-2 .item-3-3 .item-3-4 .item-3-5 .item-3-6 {
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
	            font-size: 8px;
				&:last-child {
					border-width: 0;
				}
			}
		}
	}
</style>
