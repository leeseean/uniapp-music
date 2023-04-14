<template>
	<view class="content">
		<view class="logo">
			<image class="image" mode="aspectFit" src="../../static/headimg_dl.jpg" />
		</view>
		<view class="title">
			<text>粒子音乐推广</text>
		</view>
		<view class="notice">
			<uni-card class="notice-card" style="margin:0; padding: 0;">
				<template v-slot:title>
					<view class="uni-card__header">
						<uni-icons type="notification" size="20"></uni-icons>
						<text class="uni-card__header-box">平台公告</text>
					</view>
				</template>
				<uni-list>
					<uni-list-item v-for="(item, index) in noticeData" :key="item">
						<template v-slot:body>
							<view class="notice-text">
								<text class="notice-index" :index="index+1">
									{{index+1}}</text>{{item}}</view>
						</template>
					</uni-list-item>
				</uni-list>
			</uni-card>
		</view>
		<view class="uni-list">
			<view class="uni-list-cell top-border">
				<view class="uni-list-cell-left">
					选择分类
				</view>
				<view class="uni-list-cell-db">
					<picker @change="bindPickerChange" :value="index" :range="data" range-key="name">
						<view v-if="data[index]" class="uni-input">{{data[index].name}}</view>
					</picker>
				</view>
			</view>
		</view>
		<view class="uni-list">
			<view class="uni-list-cell">
				<view class="uni-list-cell-left">
					选择商品
				</view>
				<view class="uni-list-cell-db">
					<picker :value="childIndex" :range="data[index].children" range-key="name">
						<view v-if="data[index].children[childIndex]" class="uni-input">
							{{data[index].children[childIndex].name}}
						</view>
					</picker>
				</view>
			</view>
		</view>
		<view class="buttons">
			<button class="button">加入购物车</button>
			<button class="button">立即购买</button>
		</view>
		<view class="statics">
			<uni-card class="statics-card" style="margin:0; padding: 0;">
				<template v-slot:title>
					<view class="uni-card__header">
						<uni-icons custom-prefix="iconfont" type="icon-data-view" size="20"></uni-icons>
						<text class="uni-card__header-box">数据统计</text>
					</view>
				</template>
				<uni-grid :square="false" :column="3" :highlight="true">
					<uni-grid-item v-for="(item, index) in statics" :index="index" :key="item.name">
						<view class="grid-item-box" style="background-color: #fff;">
							<template>
								<text v-if="item.type === 'money' || item.type ==='money1'"
									class="text">{{staticsData[item.type]}}元</text>
								<text v-else-if="item.type === 'yxts'" class="text">{{staticsData[item.type]}}天</text>
								<text v-else-if="item.type === 'site'" class="text">{{staticsData[item.type]}}个</text>
								<text v-else class="text">{{staticsData[item.type]}}件</text></template>
							<uni-icons class="statics-icons" custom-prefix="iconfont" :type="item.icon" :size="30"
								color="#65b1c9" />
							<text class="text">{{item.name}}</text>
						</view>
					</uni-grid-item>
				</uni-grid>
			</uni-card>
		</view>
		<view class="footer">
			<uni-card class="footer-card" is-full style="margin:0; padding: 0;">
				<view class="uni-h6">
					<text>粒子音乐推广 </text>
					<uni-icons class="icon-heart-filled" size="14" type="heart-filled" color="red"></uni-icons>
					<text>2019</text> <text class="footer-seprate">|</text> <uni-link color="#337ab7"
						class="footer-link" href="https://uniapp.dcloud.io/"
						text="https://uniapp.dcloud.io/"></uni-link>
				</view>
			</uni-card>
		</view>
	</view>
</template>

<script>
	import data from '@/common/products.js'
	import statics from '@/common/statics.js'
	export default {
		data() {
			return {
				data,
				statics,
				// staticsData 从接口取的
				staticsData: {
					cart_count: 0,
					code: 0,
					gift: null,
					money: 104290.26,
					money1: 0,
					orders: 924,
					orders1: 68,
					orders2: 0,
					site: 400,
					yxts: 372
				},
				noticeData: [
					' 温馨提示：请勿重复下单哦！必须要等待前面任务订单完成才可以下单！',
					// ' 下单之前请一定要看完该商品的注意事项再进行下单！',
					' 所有业务全部恢复，都可以正常下单，欢迎尝试，有问题可以联系客服(QQ:1111112584)',
					' 一般下单后会在1-30分钟内提交到服务器，请耐心等待！'
				],
				index: 0,
				childIndex: 0,
			}
		},
		onLoad() {

		},
		methods: {
			bindPickerChange: function(e) {
				console.log('picker发送选择改变，携带值为', e.detail)
				this.index = e.detail.value
			},
		}
	}
</script>

<style lang="scss">
	$logoHeight: 125rpx;
	$borderColor: #c8c7cc;

	.top-border {
		border-top: 1px solid $borderColor;
	}

	@media (min-width: 750px) {
		.content {
			width: 750px;
			margin: 0 auto;
		}
	}

	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 0 12rpx 6rpx 12rpx;

		.uni-list {
			.uni-list-cell {
				color: #555;
				text-align: center;
				background-color: #eee;
				border: 1px solid $borderColor;
				border-radius: 4px;
				border-top-right-radius: 0;
				border-bottom-right-radius: 0;
				border-top: none;
				border-bottom: none;

				&.top-border {
					border-top: 1px solid $borderColor;
				}
			}
		}

	}

	.buttons {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;

		.button {
			width: 50%;
			color: #fff;
			background-color: #5cb85c;
			border-color: #4cae4c;
			border-radius: 4px;
			margin-top: 20rpx;
			margin-bottom: 20rpx;

			&:nth-of-type(1) {
				border-top-right-radius: 0;
				border-bottom-right-radius: 0;
			}

			&:nth-of-type(2) {
				border-top-left-radius: 0;
				border-bottom-left-radius: 0;
				background-color: #337ab7;
				border-color: #2e6da4;
			}
		}
	}

	.logo {
		background-image: url('@/static/userbg.jpg');
		background-size: contain;
		width: 100%;
		height: $logoHeight;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: top;

		.image {
			opacity: .9;
			width: $logoHeight;
			height: $logoHeight;
			border-radius: 50%;
		}
	}

	.notice {
		width: 100%;
		margin-bottom: 20rpx;

		.notice-card {
			.notice-index {
				padding: 0 5px;
				font-size: 14px;
				border-radius: 3px;
				color: #fff;
				background-color: #d9534f;
				border-color: #d43f3a;

				&[index="2"] {
					background-color: #5cb85c;
					border-color: #4cae4c;
				}

				&[index="3"] {
					background-color: #5bc0de;
					border-color: #46b8da;
				}

				&[index="4"] {
					background-color: #f0ad4e;
					border-color: #eea236;
				}
			}

			.notice-text {
				font-size: 14px;
			}
		}
	}

	.statics {
		width: 100%;

		.statics-icons {
			margin: 5rpx 0;
		}

		.statics-card {
			border-color: #337ab7;
		}

		.uni-card__header {
			display: flex;
			border-bottom: 1px #EBEEF5 solid;
			flex-direction: row;
			align-items: center;
			padding: 10px;
			overflow: hidden;
			background-color: #337ab7;

			.uni-card__header-box {
				display: flex;
				flex: 1;
				flex-direction: row;
				align-items: center;
				overflow: hidden;
				margin-left: 10px;

				.uni-card__header-content {
					display: flex;
					flex-direction: column;
					justify-content: center;
					flex: 1;
					overflow: hidden;

					.uni-card__header-content-title {
						color: #000000;
					}
				}
			}
		}
	}

	.uni-card__header {
		display: flex;
		border-bottom: 1px #EBEEF5 solid;
		flex-direction: row;
		align-items: center;
		padding: 10px;
		overflow: hidden;
		background-color: #337ab7;

		.uni-card__header-box {
			display: flex;
			flex: 1;
			flex-direction: row;
			align-items: center;
			overflow: hidden;
			margin-left: 10px;

			.uni-card__header-content {
				display: flex;
				flex-direction: column;
				justify-content: center;
				flex: 1;
				overflow: hidden;

				.uni-card__header-content-title {
					color: #000000;
				}
			}
		}
	}

	.grid-item-box {
		flex: 1;
		// position: relative;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 15px 0;
	}

	.grid-item-box-row {
		flex: 1;
		// position: relative;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		align-items: center;
		justify-content: center;
		padding: 15px 0;
	}

	.title {
		font-size: 48rpx;
		color: #23527c;
		margin-top: 20rpx;
		margin-bottom: 20rpx;
	}

	.footer {
		margin-top: 30rpx;
		width: 100%;
		text-align: center;

		.footer-seprate {
			margin: 0 8rpx;
		}

		.footer-link {
			color: #337ab7;
		}

		.icon-heart-filled {
			margin: 0 4rpx;
		}
	}
</style>