<template>
	<view>
		<text>检查费用: {{inspcost}}\n</text>
		<text>样品数量: {{sampnum}}\n</text>
		<text>上门取样: {{isdoor}}\n</text>
		<text>取样费用: {{samprice}}\n</text>
		<text>疫情期间上门收样样品服务费 \n</text>
		<text>合计费用 : {{totalcost}}\n</text>
		<button class="mini-btn" type="warn" size="mini" @click="back">返回</button>
		<button class="mini-btn" type="default" size="mini" @click="submit">确定</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				inspcost : 0,//检测费用
				sampnum : '', // 样品数量 
				isdoor: '', //是否上门取样,
				samprice: 5, // 取样费用
				totalcost: 0, //合计费用
				entrustedUnit : '' //委托单位 
			}
		},
		onShow(options){
			uni.getStorage({
				key: 'data',
				success: (result) => {
					if (result) {
						this.inspcost = result.data.inspcost
						this.sampnum = result.data.sampnum
						this.entrustedUnit = result.data.company
						this.isdoor = '是'
						this.totalcost = this.inspcost + this.samprice

					}
				}
			});
		},
		methods: {
			submit() {
				let orderNumber = 'X20203080014'
                let inspecPerson = '13824462248'
				let entrustedUnit = '青城市公安局'
				uni.setStorage({
					key:"data",
					data:{
						totalcost : 100,
						orderNumber: orderNumber,
						inspecPerson : inspecPerson,
						entrustedUnit : entrustedUnit,
						orderTime :  "2020-03-09 10:34:06"
					}
				})
				uni.navigateTo({
					url : 'payOrder'
				})
			},
			back() {
				uni.navigateBack({
					url: 'sampleRegistration'
				})
			}
		}
	}
</script>

<style>

</style>
