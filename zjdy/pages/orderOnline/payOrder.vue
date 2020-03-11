<template>
	<view>
		<text>订单编号: {{orderNumber}} \n</text>
		<text>送检人员: {{inspecPerson}} \n</text>
		<text>委托单位: {{entrustedUnit}} \n</text>
		<text>下单时间: {{orderTime}} \n</text>
		<text>总金额: ¥ {{totalprice}} \n</text>
		<text>剩余支付时间:  {{timer}} \n</text>
		<text>支付成功不予退款  \n</text>
		<text>微信支付 \n</text>
		<text>余额支付 \n</text>
		
	    <button class="mini-btn" type="warn" size="mini" @click="laterpay">稍后付款</button>
		<button class="mini-btn" type="default" size="mini" @click="pay">付款</button>
	</view>
</template>

<script>
	import uniCountdown from "@/components/uni-countdown/uni-countdown.vue"

	export default {
		data() {
			return {
				orderNumber :'',//订单编号
				entrustedUnit :'',//委托单位
				inspecPerson : '',//送检人员
				orderTime : '', //下单时间
				totalprice : 0 , //总金额
				timer:''
			}
		},
		onLoad() {			
		},
		onShow() {
			uni.getStorage({
				key: 'data',
				success: (result) => {
					this.orderNumber = result.data.orderNumber
					this.entrustedUnit = result.data.entrustedUnit 
					this.inspecPerson = result.data.inspecPerson
					this.totalprice = result.data.totalprice
					this.orderTime = result.data.orderTime
				},
			})
			
			var hour = 0, minute = 59, second = 59; /*时 分 秒*/
			var millisecond = 0; //毫秒
			var timers = setInterval(() => {
				millisecond = millisecond + 50;
				if (millisecond >= 1000) {
					millisecond = 0;
					second = second - 1;
				}
				if (second <= 0) {
					second = 59;
					minute = minute - 1;
				}
                 if (minute < 0) {
					  clearInterval(timers)
					  minute = 0
					  second = 0
                      //this.back()
				 }
				this.timer = minute+'分'+second+'秒';
			}, 50);
		},
		methods: {
			back() {
				clearInterval(this.timer)
				// uni.navigateTo({
					
				// 	url: 'sampleRegistration'
				// })
			},
			laterpay() {
				
			},
			pay() {
				
			}
		}
	}
</script>

<style>

</style>
