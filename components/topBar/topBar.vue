<template>
	<view class="box">
		<div class="left" @click="open">
			<image src="../../static/icon-location.png" mode="" class="locationImg"></image>
			<text>{{city}}</text>
		</div>
		<div class="mid">
			<u-icon name="search" color="#ebebeb" size="28" @click="search"></u-icon>
			<u-input class="uinpt" placeholderStyle="font-size: 13px;" v-model="searchInfo" @confirm="onEnter"
				placeholder="搜索医院、科室、疾病、医生" />
		</div>
		<div class="right">
			<image @click="navigateToMessage" class="mesImg" src="../../static/icon-message.png" mode=""></image>
		</div>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				city: "天津",
				searchInfo: '',

			}
		},
		methods: {
			navigateToMessage() {
				uni.navigateTo({
					url: '/pages/chatGPT/chatGPT'
				})
			},
			search() {
				console.log(this.searchInfo);
				// 向后端发送查询
			},
			onEnter() {
				this.search();
			},
			open() {
				uni.navigateTo({
					url: '/pages/map/map'
				})
			},
			onUnload() {
				// 在页面渲染之前获取localStorage的值并更新city
				uni.getStorage({
					key: 'location',
					success: function (res) {
						console.log(res.data);
						if (location) {
							this.city = location;
						}
					}
				});

			},
		},
	}
</script>

<style lang="less" scoped>
	.map-container {
		width: 100%;
		height: 80vh;
	}

	.box {
		display: flex;
		flex-direction: row;
		margin: 30px 5px 10px 5px;
		justify-content: space-evenly;
		align-items: center;
		padding: 5px;
		box-shadow: 3px 3px 10px rgba(0, 0, 0, 0.2);
		border-radius: 8px;

		.left {
			display: flex;
			flex-direction: row;
			align-items: center;

			.locationImg {
				width: 40px;
				height: 40px;
				margin-right: 5px;
			}

		}

		.mid {
			display: flex;
			border: 1px solid #ebebeb;
			border-radius: 5px;

			/deep/.uinpt {
				border: none;
			}

		}

		.right {
			.mesImg {
				width: 30px;
				height: 30px;
			}
		}
	}
</style>