<template style="background-color: #000000;">
	<view>
		<view class="uni-form-item uni-column">
			<view class="title">委托单位:</view>
			<input class="uni-input" name="input" @click="getEntrustedUnit()" :value="company" placeholder="请选择委托单位" />
		</view>
		<view class="uni-form-item uni-column">
			<view class="title">单位地址：</view>
			<input class="uni-input" name="input" :value="addr" placeholder="请输入单位地址" />
		</view>
		<view class="button-sp-area">
			<button type="primary" @click="appendSample">增加样品</button>
		</view>
		<view>
			<ul>
				<li v-for="(sam,index) in samples" :key="sam.id">
					<view>
						<text>
							{{ index + 1 }}
						</text>
						<text>
							样品名称： {{ sam.name }}
						</text>
						<text>
							检查项目： {{ sam.project }}
						</text>
						<text>
							价格： {{ sam.price }}
							
						</text>
						<button type="warn" size = "mini" @click="del(index,sam.price)" >删除</button>
					</view>
				</li>
			</ul>

		</view>

		<view>
			<view>
				<text>
					样品数量：{{ sampleNum }}
				</text>
				<text>
					检测项目：{{ projecNum }}
				</text>
				<text>
					合计：{{ totalprice }}
				</text>
			</view>

			<view class="button-sp-area">
				<button type="primary" @click="cancel">取消</button>
			</view>
			<view class="button-sp-area">
				<button type="primary" @click="submit">提交订单</button>
			</view>
		</view>
	</view>
</template>

<script>
	const sample = {
		id: '',
		name: '',
		price: 0,
		project: ''
	}

	export default {
		data() {
			return {
				company: '',
				addr: '',
				samples: [],
				sampleNum: 0,
				projecNum: 0,
				totalprice: 0

			}
		},
		onLoad: function(option) {
			help()
		},
		onShow(result) {

			uni.getStorage({
				key: 'data',
				success: (result) => {
					console.log(result.data.sample)
					if (result.data.unit) {
						this.company = result.data.unit
						this.addr = result.data.addr
					}
					if (result.data.sample.id != null) {
						for(let i =0;i<this.samples.length;i++){
							if(this.samples[i].id === result.data.sample.id){
								return ;
							}
						}
						this.samples.push(result.data.sample)
						this.sampleNum ++
						this.projecNum ++
						this.totalprice = this.totalprice + result.data.sample.price
					}
				}
			});

		},
		methods: {
			getEntrustedUnit() {
				uni.navigateTo({
					url: 'selectEntrustedUnit'
				})
			},
			appendSample() {
				uni.navigateTo({
					url: 'addSample'
				})
			},
			cancel() {
				uni.showModal({
					title: '提示',
					content: '您有订单未提交，确定返回上一页吗',
					success: function(res) {
						if (res.confirm) {
							console.log('用户点击确定');
						} else if (res.cancel) {
							console.log('用户点击取消');
						}
					}
				})
			},
			submit() {
				let message = ''
				if (this.company === '') {
					uni.showToast({
						title: '请先登记样品',
						mask: true,
						icon: 'none',
						duration: 2000
					});
				}
				     uni.setStorage({
				     	key: 'data',
						data: {
							inspcost : this.totalprice,
							sampnum : this.sampleNum,
							company : this.company 
						}
				     })
                     uni.navigateTo({
                     	url:'confirOrder'
                     })
			},
			del(index,price) {
				console.log(price)
				this.samples.splice(index,1)
				this.sampleNum --
				this.projecNum --
				this.totalprice = this.totalprice - price
			},
			help() {
				this.company = ''
				this.addr = ''
				this.sample = ''
				this.samples = ''
			}
		}

	}
</script>

<style>
</style>
