<template>
	<view>
		<view class="uni-padding-wrap">
			<view class="page-section swiper">
				<view class="page-section-spacing">
					<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
						<swiper-item>
							<view class="swiper-item uni-bg-red">
								<image src="../../static/img/common/bg.png" mode="scaleToFill" class="img"></image>
							</view>
						</swiper-item>
						<swiper-item>
							<image src="../../static/img/common/bg.png" mode="scaleToFill" class="img"></image>
						</swiper-item>
						<swiper-item>
							<image src="../../static/img/common/bg.png" mode="scaleToFill" class="img"></image>
						</swiper-item>
					</swiper>
				</view>
			</view>
		</view>
		<view class="nav-list">
			<view class="nav-enter">
				<image src="../../static/img/common/1.png" mode="aspectFit" @click="orderOnline" class="logoimg"></image>
				<view>
				<text>自助下单</text>
				</view>
			</view>
			<view class="nav-enter">
				<image src="../../static/img/common/2.png" mode="aspectFit" @click="orderInquiry" class="logoimg"></image>
				<view>
					<text>订单查询</text>
				</view>
			</view>
			<view class="nav-enter">
				<image src="../../static/img/common/3.png" mode="aspectFit" @click="myInfo" class="logoimg"></image>
				<view>
					<text>个人中心</text>
				</view>
			</view>
			<view class="nav-enter">
				<image src="../../static/img/common/4.png" mode="aspectFit" class="logoimg"></image>
				<view>
					<text>自助下单</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 20000
			}
		},
		methods: {
			orderOnline() {
				uni.navigateTo({
					url:'../orderOnline/sampleRegistration'
				})
			},
			orderInquiry() {
				uni.navigateTo({
					url:'../orderInquiry/trackOrder'
				})
			},
             myInfo() {
				uni.navigateTo({
					url:'../myInfo/ucenter'
				})
			}
		}
	}
</script>

<style>
	.intro {
		font-size: 14px;
		line-height: 24px;
	}

	.img {
		width: 100%;

	}

	.logoimg {
		width: 150rpx;
		height: 150rpx;
		border-radius: 50%;
		margin-left: 5%;
		margin-top: 10%;
	}
	.nav-list{
		margin-top: 5%;
		display:flex;
	}
	.nav-enter{
		display: flexbox;
		width:25%;
		text-align: center;
	}
</style>
