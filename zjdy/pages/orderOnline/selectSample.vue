<template>
	<view>
		<view id="top-text" class="uni-form-item uni-column">
			<input class="uni-input" name="input" v-model="sample.name" @input="getSample()"  placeholder="请输入关键字" />
		</view>
		<view id="bottom-text">
			<ul id="example-1">
			  <li v-for="sam in samples" >
				<scroll-view scroll-y="ture" refresher-enabled="true">
				<text @click="setInputname(sam)">
			    {{ sam.name }}
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
				sample:{
					id: '',
					name: '',
					price: 0,
					project: ''
				},
				samples:[]
			}
		},
		methods: {
			getSample() {
	            for(let i=1;i< 100;i++){
					this.samples.push({id:i,name:'西红柿'+i,price:i,project:'农药残留'})
				}
			},
			setInputname(sample) {
				console.log(sample)
				uni.setStorage({
					key: 'data',
					data: {
						sample : sample,
						}
				})
				uni.navigateBack({
					url: 'addSample'
					
				})
			}
		}
	
	}
</script>

<style>
</style>
