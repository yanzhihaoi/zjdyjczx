<template>
	<view>
		<view>账户余额：{{restMoney}} 元\n</view>
		<view>预存金额：{{preMoney}} 元\n</view>
		<view>赠送金额：{{presenterMoney}} 元\n</view>
		<button type="primary" @click="recharge">充值</button>
		<button type="primary" @click="resetPwd">重置支付密码</button>
		<button type="primary" @click="billflow">账单流水</button>
		<button type="primary" @click="myinfo">个人信息</button>
		<button type="primary" @click="groupmanage">分组管理</button>
		
		<uni-popup ref="showtip" :type="type" :mask-click="false" >
			<view class="uni-tip">
				<text class="uni-tip-title">重置支付密码</text>
				<input v-model="password" placeholder="设置6位纯数字密码" class="is-input1"   data-val="password"/>
				<input v-model="truepassword" placeholder="验证6位纯数字密码" class="is-input1"   data-val="password"/>				
				<view class="uni-tip-group-button">
					<text class="uni-tip-button" @click="cancel()">取消</text>
					<text class="uni-tip-button" @click="submit()">确定</text>
				</view>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import uniPopup from "@/components/uni-popup/uni-popup.vue"
	export default {
		components: {uniPopup},
		data() {
			return {
				restMoney:'', // 账户余额
				preMoney:'', // 预存金额
				presenterMoney:'', // 赠送金额
				password:'',
				truepassword:''
			}
		},
		onShow() {
			this.restMoney = '100'
			this.preMoney = '300'
			this.presenterMoney = '10000'
		},
		methods: {
			recharge() {
				console.log("充值")
			},
			resetPwd() {
				console.log("重置支付密码")
				this.$nextTick(() => {
					this.$refs['showtip'].open()
				})
			},
			billflow() {
				uni.navigateTo({
					url:'billflow'
				})
			},
			myinfo() {
				uni.navigateTo({
					url:'myinfo'
				})
			},
			groupmanage() {
				console.log("分组管理")
			},
			cancel() {
				this.$refs['showtip'].close()
			},
			submit() {
				console.log(this.password)
				console.log(this.truepassword)
				this.$refs['showtip'].close()
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
