<template>
	<view class="container">
		<view class="top">
			<text id="title">注册</text>
			<text id="tips">请告诉我们，您的手机号码</text>
		</view>
		<view class="info">
			<u-form :model="form" ref="uForm">
				<u-form-item prop="phone"><u-icon name="phone" color="#2979ff" size="28"></u-icon>
					<u-input v-model="form.phone" placeholder="请输入手机号码" class="login-input" /></u-form-item>
				<u-form-item><u-button @click="send" class="login-button">下一步</u-button></u-switch></u-form-item>
			</u-form>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				form: {
					phone: '',
				},
				rules: {
					phone: [{
						required: true,
						message: '请输入手机号码',
						trigger: ['blur'],
					}],
				}
			};
		},
		methods: {
			send() {
				console.log("发送验证码",this.form.phone);
				// 向下一个页面发送消息
				uni.$emit("sendPhone",this.form.phone)
			}
		},
		onReady() {
			this.$refs.uForm.setRules(this.rules);
		}
	}
</script>

<style lang="less" scoped>
	.container {
		display: flex;
		justify-content: center;
		flex-direction: column;
		align-items: center;

		.top {
			display: flex;
			flex-direction: column;
			justify-content: left;
			width: 70vw;

			#title {
				font-size: 30px;
				font-weight: bold;
				margin-top: 10px;
			}

			#tips {
				font-weight: 600;
				margin-top: 10px;
			}
		}

		.info {
			margin-top: 30px;
			width: 70vw;

			.login-input {
				border: none;
				padding: 10px;
				border-bottom: 1px solid #f7ecdf;
			}

			.login-button {
				margin-top: 40px;
				background-color: #2979ff;
				color: #fff;
				text-align: center;
				border-radius: 20px;
				font-size: 17px
			}
		}
	}
</style>