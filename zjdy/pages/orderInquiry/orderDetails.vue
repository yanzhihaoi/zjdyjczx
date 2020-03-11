<template>
	<view>
		<view>下单凭证：\n</view>
		<view>
			<text>订单编号：{{orderNum}} \n</text>
			<text>委托单位：{{entrustedUnit}}\n</text>
			<text>送检单位：{{inspUnit}}\n</text>
			<text>联系电话：{{phone}}\n</text>
			<text>订单金额：{{orderPay}}\n</text>
			<text>下单时间：{{orderTime}}\n</text>
			<text>付款时间：{{payTime}}\n</text>
			<text>订单状态：{{orderState}}\n</text>
			<text>交易单号：{{transNumber}}\n</text>
			
		</view>
		<view>=========================================================</view>
		<view>
			<ul>
				<li v-for="(sam,index) in samples" :key="sam.id">
					<text @click="printReportCode">
						打印报告码\n
					</text>
					<text @click="checkReport">
						检测报告\n
					</text>
					<text>
						{{ index + 1 }}\n
					</text>
					<text>
						样品名称： {{ sam.samname }}\n
					</text>
					<text>
						检查项目： {{ sam.project }}\n
					</text>
					<text>
						价格： {{ sam.price }}\n
						
					</text>
					<text>
						状态： {{ sam.state }}\n
						==========================
					</text>
				</li>
			</ul>
		</view>
		
		<uni-popup ref="showtip"  :mask-click="false" @change="change">
			<view class="uni-tip">
				<image src="../../static/img/common/testcode.png" style="width: 50px;height: 50px;"></image>
				<text class="uni-tip-title"></text>
				<text class="uni-tip-content">打印报告码：EBQQKW</text>
				<view class="uni-tip-group-button">
					<text class="uni-tip-button" @click="cancel('tip')">关闭</text>
				</view>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import uniPopup from '@/components/uni-popup/uni-popup.vue'
	export default {
		components: {
			uniPopup
		},
		data() {
			return {
				orderNum:'',      //订单编号
				entrustedUnit:'', //委托单位
				inspUnit:'',    //送检单位
				phone: '',     //联系电话
				orderPay: '' ,//订单金额
				orderTime:'',//下单时间
				payTime:'', //付款时间
				orderState:'',//订单状态
				transNumber:'',//交易单号
				samples : []
			}
		},
		onShow() {
			console.log("onshow")
			this.orderNum = 'x20200000'
			this.entrustedUnit = '送检单位组 [2]'
			this.inspUnit = '广州达元信息科技有限公司'
			this.phone = '13824462248'
			this.orderPay = '20元'
			this.orderTime = '2020-02-27 15:45:48'
			this.payTime = '2020-02-27 15:45:48'
			this.orderState = '已付款'
			this.transNumber = '10034202000202124241'
			this.samples = [
				{samname:'西瓜子' ,price:'¥0.01',project:'二氧化碳',state:'合格'},
				{samname:'红樱桃' ,price:'¥0.01',project:'二氧化碳',state:'合格'}
			] 
		},
		methods: {
			printReportCode() {
				this.$nextTick(() => {
					this.$refs['showtip'].open()
				})
			},
			checkReport() {
				uni.navigateTo({
					url:'checkReport'
				})
			},
			cancel(type) {
				this.$refs['show' + type].close()
			},
			change(e) {
				console.log('是否打开:' + e.show)
			}
		}
	}
</script>

<style>
/* 提示窗口 */
	.uni-tip {
		/* #ifndef APP-NVUE */
		display: flex;
		flex-direction: column;
		/* #endif */
		padding: 15px;
		width: 300px;
		background-color: #fff;
		border-radius: 10px;
		margin-top: 30%;
		margin-left: 10%;
	}

	.uni-tip-title {
		margin-bottom: 10px;
		text-align: center;
		font-weight: bold;
		font-size: 16px;
		color: #333;
	}

	.uni-tip-content {
		/* padding: 15px;
 */
		font-size: 14px;
		color: #666;
	}

	.uni-tip-group-button {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		margin-top: 20px;
	}

	.uni-tip-button {
		flex: 1;
		text-align: center;
		font-size: 14px;
		color: #3b4144;
	}
</style>
