<template>
	<view>
		<view id="top-text" class="uni-form-item uni-column">
			<input class="uni-input" name="input" v-model="inputname" @input="getEntrustedUnit()"  placeholder="请输入关键字" />
		</view>
		<view id="bottom-text">
			<ul id="example-1">
			  <li v-for="unit in units" >
				<scroll-view scroll-y="ture" refresher-enabled="true">
				<text @click="setInputname(unit)">
			    {{ unit }}
				</text>
				</scroll-view>
			  </li>
			</ul>

		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				units:[],
				inputname:''
			}
		},
		methods: {
			getEntrustedUnit() {
				console.log("获取委托单位:" + this.inputname)
                for(let i=1;i< 100;i++){
					this.units.push("第"+i+"个单位")
				}

			},
			setInputname(company) {
				console.log(company)
				uni.setStorage({
					key: 'data',
					data: {
						unit : company,
						addr : '关公庙',
						sample : '',
						}
				})
				uni.navigateBack({
					url: 'sampleRegistration'
					
				})
			}
		}
	
	}
</script>

<style>
</style>
