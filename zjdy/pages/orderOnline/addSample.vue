<template>
	<view>
		<view class="uni-form-item uni-column">
			<view class="title">选择样品:</view>
			<input class="uni-input" name="input" @click="select" v-model="simple.name" placeholder="选择样品" />
		</view>
		<view class="uni-form-item uni-column">
			<view class="title">检测项目:</view>
			<input class="uni-input" name="input" v-model="simple.project" />
			<view> {{ simple.price }}</view>
		</view>
		<view @tap="viewdetails">
			<text>送检样品至少保留100~250克，并独立包装，否则视为无效样品。
					<text style="color: #ff5500;">查看详情？</text>
				）</text>
		</view>

		<view class="button-sp-area">
			<button type="primary" @click="back">取消</button>
		</view>
		<view class="button-sp-area">
			<button type="primary" @click="submit">确定</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				simple: {
					id: '',
					name: '',
					project: '',
					price: 0
				}
			}
		},
		onLoad() {
			this.help()
		},
		onShow(result) {
			uni.getStorage({
				key: 'data',
				success: (result) => {
					if (result) {
						this.simple = result.data.sample
					}
				}
			});

		},
		onReady() {
			this.help()
		},
		methods: {
			select() {
				uni.navigateTo({
					url: 'selectSample'
				})
			},
			viewdetails() {
				console.log("22")
				uni.navigateTo({
					url: 'sampleNorms'
				})
			},
			back() {
				uni.navigateBack({
					url: 'sampleRegistration'
				})
			},
			submit() {
				console.log(this.simple)
				if (this.simple.id === '') {
					uni.showToast({
						title: '请至少选择一种检测项目',
						mask: true,
						icon: 'none',
						duration: 2000
					});
				}
				uni.setStorage({
					key: 'data',
					data: {
						unit: '',
						addr: '',
						sample: this.simple
					}
				})
				uni.navigateBack({
					url: 'sampleRegistration'

				})
			},
			help() {
				this.simple= {id:'',name: '',project: '',price: 0}
			}

		}
	}
</script>

<style>
</style>
