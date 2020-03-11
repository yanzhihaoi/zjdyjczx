<template>
	<!-- <section class="Index-Page">
		<s-tabs :effect="false" v-model="activeTab" @change="change" :nav-per-view="2">
			<s-tab title="<span>交易明细</span>">
				<view  hidden= true>
					<ul>
						<li v-for="(det , index) in detailsList " :key="det.id">
							 <text>序号{{index + 1}} \n</text>
                             <text>{{det.costType}} \n</text>
							 <text>检测类型{{det.inscost}} \n</text>
							 <text>花费金额{{det.spend}} \n</text>
							 <text>花费金额{{det.paytime}} \n</text>
							 <text>余额{{det.balance}} \n</text>
							 <text v-if="det.costType === '余额充值'">
								 赠送金额：{{det.giftAmount}} \n
							 </text>
							 <text>==============================</text>
						</li>						
					</ul>
				</view>
			</s-tab>
			<s-tab title="<span>充值记录</span>">
			<view>
				<ul>
					<li v-for="(det , index) in rechargedList " :key="det.id">
						 <text>序号{{index + 1}} \n</text>
			             <text>{{det.costType}} \n</text>
						 <text>检测类型{{det.inscost}} \n</text>
						 <text>花费金额{{det.spend}} \n</text>
						 <text>花费金额{{det.paytime}} \n</text>
						 <text>余额{{det.balance}} \n</text>
						 <text v-if="det.costType === '余额充值'">
							 赠送金额：{{det.giftAmount}} \n
						 </text>
						 <text>==============================</text>
					</li>						
				</ul>
			</view>
			</s-tab>

		</s-tabs>
	</section> -->
	
	<view class="container999" @touchstart="refreshStart" @touchmove="refreshMove" @touchend="refreshEnd">
		<!-- 刷新组件需搭配scroll-view使用，并在pages.json中添加 "disableScroll":true-->
		<refresh ref="refresh" @isRefresh='isRefresh'></refresh>
		<view class='nav'>
			<!-- #ifdef H5 -->
			<view style="height: 44px;width: 100%;">边距盒子</view>
			<!-- #endif -->
	
			<!-- 导航栏 agents导航栏标题 -->
			<navTab ref="navTab" :tabTitle="tabTitle" @changeTab='changeTab'></navTab>
		</view>
	
		<!-- swiper切换 swiper-item表示一页 scroll-view表示滚动视窗 -->
		<swiper style="min-height: 100vh;" :current="currentTab" @change="swiperTab">
			<swiper-item v-for="(listItem,listIndex) in list" :key="listIndex">
				<scroll-view style="height: 100%;" scroll-y="true" @scrolltolower="lower1" scroll-with-animation :scroll-into-view="toView">
					<view :id="'top'+listIndex" style="width: 100%;height: 180upx;">边距盒子</view>
					<view class='content'>
						<view class='card' v-for="(det , index) in listItem" v-if="listItem.length > 0" :key="index">
						
									 <text>序号{{index + 1}} \n</text>
									 <text>{{det.costType}} \n</text>
									 <text>检测类型{{det.inscost}} \n</text>
									 <text>花费金额{{det.spend}} \n</text>
									 <text>花费金额{{det.paytime}} \n</text>
									 <text>余额{{det.balance}} \n</text>
									 <text v-if="det.costType === '余额充值'">
										 赠送金额：{{det.giftAmount}} \n
									 </text>
									 <text>==============================</text>

						</view>
					</view>
					<view class='noCard' v-if="listItem.length===0">
						暂无信息
					</view>
					<view style="width: 100%;height: 100upx;opacity:0;">底部占位盒子</view>
				</scroll-view>
			</swiper-item>
		</swiper>
		<!-- 		<tabBar4 :currentPage="currentPage"></tabBar4> -->
	</view>
</template>

<script>
	import sTabs from '@/s-ui/s-tabs';
	import sTab from '@/s-ui/s-tab';
	const util = require('../../static/util/util.js');
	import refresh from '../../components/refresh.vue';
	import navTab from '../../components/navTab.vue';
	import tabBar4 from '../../components/tabBar4.vue';


	export default {
		components: {
			refresh,
			navTab,
			tabBar4
		},
		components: {
			sTabs,
			sTab
		},
		data() {
			return {
				activeTab: 0,
				detailsList: [],
				rechargedList: [],
				ishidden : false,
				currentPage: 'index',
				toView: '', //回到顶部id
				tabTitle: ['交易明细', '充值记录'], //导航栏格式 --导航栏组件
				currentTab: 0, //sweiper所在页
				pages: [1, 1], //第几个swiper的第几页
				list: [
					[],
					[]
				]
			};
		},
		onShow() {
			let list1 = [{
				    costType: '检测费用',
					inscost: 10,
					payType: '余额支付',
					spend: -10,
					paytime: '2020-02-27',
					balance: 10
				},
				{
					costType: '检测费用',
					inscost: 11,
					payType: '余额支付',
					spend: -10,
					paytime: '2020-02-27',
					balance: 10
				},
				{
					costType: '检测费用',
					inscost: 12,
					payType: '余额支付',
					spend: -10,
					paytime: '2020-02-27',
					balance: 10
				},
				{
					costType: '检测费用',
					inscost: 13,
					payType: '余额支付',
					spend: -10,
					paytime: '2020-02-27',
					balance: 10
				},
				{
					costType: '余额充值',
					inscost: 14,
					payType: '微信支付',
					spend: -10,
					paytime: '2020-02-27',
					balance: 10,
					giftAmount: 10
				}
			]
			this.list[0] = list1
			for(let i = 0;i<list1.length;i++){
				if( list1[i].costType === '余额充值' ){
					this.list[1].push(list1[i])
				}
			}

		},
		methods: {
			change(index) {
				if(index === '0'){
					this.ishidden = true
				}else{
					this.ishidden = false
				}
				
				console.log(index);
			},
			toTop() {
				this.toView = ''
				setTimeout(() => {
					this.toView = 'top' + this.currentTab
				}, 10)
			},
			changeTab(index) {
				this.currentTab = index;
			},
			// swiper 滑动
			swiperTab: function(e) {
				var index = e.detail.current //获取索引
				this.$refs.navTab.longClick(index);
			},
			// 加载更多 util.throttle为防抖函数
			lower1: util.throttle(function(e) {
			}, 300),
			// 刷新touch监听
			refreshStart(e) {
				this.$refs.refresh.refreshStart(e);
			},
			refreshMove(e) {
				this.$refs.refresh.refreshMove(e);
			},
			refreshEnd(e) {
				this.$refs.refresh.refreshEnd(e);
			},
			isRefresh() {
				setTimeout(() => {
					uni.showToast({
						icon: 'success',
						title: '刷新成功'
					})
					this.$refs.refresh.endAfter() //刷新结束调用
				}, 1000)
			}
		}
	};
</script>

<style lang="scss">
	.Index-Page {
		.s-tab-wrap {
			height: 600rpx;
			padding: 40rpx;
			font-size: 28rpx;
		}
	}
	
	
	.container999 {
		width: 100vw;
		font-size: 28upx;
		min-height: 100vh;
		overflow: hidden;
		color: #6B8082;
		position: relative;
		background-color: #f6f6f6;
	}
	
	.content {
		width: 100%;
	}
	
	.card {
		width: 90%;
		height: 368upx;
		background-color: white;
		margin: 0 auto 42upx auto;
		background: #FFFFFF;
		box-shadow: 0 0 5px 0 rgba(0, 0, 0, 0.10);
		border-radius: 5px;
		position: relative;
	}
	
	.noCard {
		width: 90%;
		height: 200upx;
		margin: auto;
		background-color: white;
		display: flex;
		align-items: center;
		justify-content: center;
		color: #999999;
		box-shadow: 0 0 10upx 0 rgba(0, 0, 0, 0.10);
		border-radius: 10upx;
	}
	
	
	.nav {
		position: fixed;
		left: 0;
		top: 0;
		color: white;
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		justify-content: flex-start;
		font-size: 24upx;
		background-color: #50B7EA;
		z-index: 996;
	}
	
	.searchInput999 {
		width: 90%;
		margin: 0 auto;
		background: white;
		border-radius: 30upx;
		display: flex;
		align-items: center;
		justify-content: center;
		height: 56upx;
	}
	
	.search999 {
		width: 32upx;
		height: 32upx;
	}
	
	.searchBox999 {
		width: 56upx;
		height: 56upx;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	
	.input999 {
		color: #999;
		width: 80%;
	}
</style>
