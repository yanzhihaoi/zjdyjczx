<template>
	<view>
		<view>手机号： <input :value='info.phone' /> \n</view>
		<view>密码： <input password='ture' :value='info.password' /> \n</view>
		<view>姓名： <input :value='info.username' /> \n</view>
		<view>用户类型：
			<view>
				<label class="radio">
					<radio value="企业" :checked="info.type === '企业'" />企业</label>
				<label class="radio">
					<radio value="个人" :checked="info.type === '个人'" />个人</label>
			</view>
		</view>
		<view>
			社会信用代码：<input :value="info.creditcode" />
		</view>
		<view>
			公司名称：<input :value="info.companyName" />
		</view>
		<view class="uni-padding-wrap uni-common-mt">
			<button type="warn" @click="wxuntying">微信解绑</button>
			<button type="primary" @click="submit">保存信息</button>
		</view>

		<uni-popup ref="showtip"  :mask-click="false" @change="change">
			<view class="uni-tip">
				<text class="uni-tip-title">消息</text>
				<text class="uni-tip-content">确定要解绑吗</text>
				<view class="uni-tip-group-button">
					<text class="uni-tip-button" @click="cancel('tip')">关闭</text>
					<text class="uni-tip-button" @click="fix()">确定</text>

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
				info: {
					phone: '',
					password: '',
					username: '',
					type: '',
					creditcode: '',
					companyName: ''
				}
			}
		},
		onShow() {
			let result = {
				phone: '13824462248',
				password: '123456',
				username: '',
				type: '企业',
				creditcode: '912421424342343',
				companyName: '广州中检达元'
			}
			console.log(result)
			this.info = result
			console.log(info)
		},
		methods: {
			wxuntying() {
				this.$nextTick(() => {
					this.$refs['showtip'].open()
				})
			},
			submit() {

			},
			flx() {
				this.$refs['showtip'].close()
				uni.reLaunch({
					url: "../login/login"
				})
			},
			cancel(type) {
				this.$refs['showtip'].close()
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
/* 		margin-top: 30%;
		margin-left: 10%; */
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
