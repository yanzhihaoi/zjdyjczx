<template>
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
						<view class='card' v-for="(item,index) in listItem" v-if="listItem.length > 0" :key="index">
							<text>{{index+1}} \n</text>
							<text>委托单位：{{item.entrustedUnit}} \n</text>
							<text @click="getOrderDetails">订单编号：{{item.orderNumber}} \n</text>
							<text>订单金额：{{item.totalprice}} \n</text>

							<text>下单时间：{{item.orderTime}} \n</text>
							<text>订单状态：{{item.state}} \n</text>

							<view v-if="item.state === '已付款'">
								<text>查看详情 \n</text>
								<text>下单凭证 \n</text>
								<text>查看报告 \n</text>
							</view>
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
	const util = require('../../static/util/util.js');
	import refresh from '../../components/refresh.vue';
	import navTab from '../../components/navTab.vue';
	import tabBar4 from '../../components/tabBar4.vue';


	const order = {
		orderNumber: '', //订单编号
		entrustedUnit: '', //委托单位
		inspecPerson: '', //送检人员
		orderTime: '', //下单时间
		totalprice: 0, //总金额
		state: ''
	}
	export default {
		components: {
			refresh,
			navTab,
			tabBar4
		},
		data() {
			return {
				currentPage: 'index',
				toView: '', //回到顶部id
				tabTitle: ['已付款', '待付款', '已取消'], //导航栏格式 --导航栏组件
				currentTab: 0, //sweiper所在页
				pages: [1, 1, 1], //第几个swiper的第几页
				list: [
					[],
					[],
					[]
				]
			};
		},
		onLoad(e) {},
		onShow() {
			for (let i = 0; i < 10; i++) {
				let order1 = {}
				//已付款
				order1.orderNumber = 'X20203080014' + i
				order1.entrustedUnit = '青城市公安局' + i
				order1.inspecPerson = '13824462248'
				order1.orderTime = '2020-03-09 10:34:06'
				order1.state = '已付款'
				order1.totalprice = '30'
				this.list[0].push(order1)
			}
			for (let i = 0; i < 10; i++) {
				let order1 = {}
				//已付款
				order1.orderNumber = 'X20203080014' + i
				order1.entrustedUnit = '青城市公安局' + i
				order1.inspecPerson = '13824462248'
				order1.orderTime = '2020-03-09 10:34:06'
				order1.state = '待付款'
				order1.totalprice = '30'
				this.list[1].push(order1)
				//待付款
				//已取消
			}
			for (let i = 0; i < 10; i++) {
				let order1 = {}
				//已付款
				order1.orderNumber = 'X20203080014' + i
				order1.entrustedUnit = '青城市公安局' + i
				order1.inspecPerson = '13824462248'
				order1.orderTime = '2020-03-09 10:34:06'
				order1.state = '已取消'
				order1.totalprice = '30'
				this.list[2].push(order1)
				//待付款
				//已取消
			}

			console.log(this.list)
		},
		onHide() {},
		methods: {
			getOrderDetails() {
                uni.navigateTo({
                	url: 'orderDetails'
                })
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
			// 其他请求事件 当然刷新和其他请求可以写一起 多一层判断。
			/* 			isRequest() {
							return new Promise((resolve, reject) => {
								this.pages[this.currentTab]++
								var that = this
								setTimeout(() => {
									uni.hideLoading()
									uni.showToast({
										icon: 'none',
										title: `请求第${that.currentTab + 1 }个导航栏的第${that.pages[that.currentTab]}页数据成功`
									})
									let newData = ['新数据1', '新数据2', '新数据3']
									resolve(newData)
								}, 1000)
							})
						}, */
			// swiper 滑动
			swiperTab: function(e) {
				var index = e.detail.current //获取索引
				this.$refs.navTab.longClick(index);
			},
			// 加载更多 util.throttle为防抖函数
			lower1: util.throttle(function(e) {
				//console.log(`加载${this.currentTab}`) //currentTab表示当前所在页数 根据当前所在页数发起请求并带上page页数
				/* 				uni.showLoading({
									title: '加载中',
									mask: true
								}) */
				/* 				this.isRequest().then((res) => {
									let tempList = this.list
									console.log("isrequest")
									tempList[this.currentTab] = tempList[this.currentTab].concat(res)
									console.log(tempList)
									this.list = tempList
									this.$forceUpdate() //二维数组，开启强制渲染
								}) */
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
