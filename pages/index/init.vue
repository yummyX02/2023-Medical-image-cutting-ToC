<template>
</template>

<script>
	export default {
		data() {
			return {
				token:'',
				value:'',
			}
		},
		

		onLoad() {
			
			// 判断操作
			let value = '';
			let token = '';
			uni.getStorage({
				key:'launchFlag',
				success:function(res){
					value = res.data;
					console.log("获取",res.data);
				}	,
				fail:function(err){
					value = err.data;
				}
			})
			uni.getStorage({
				key: "access_token",
				success: function(res) {
					console.log("请求成功", res);
					token = res.data;
				},
				fail: function(err) {
					console.log(err);
					token = err.data;
				}
			})
			if (value) {
				console.log("不是第一次进入app",value);
				if (token) { //有token
					console.log("有token");
					setTimeout(function() {
						uni.switchTab({
							url: '/pages/index/home',
						});
					}, 100)
				} else {
					console.log("没有token，即将跳转登录页");
					setTimeout(function() { //去登录
						uni.reLaunch({
							url: '/pages/login/login',
						});
					}, 100)
				}
			} else {
				// 没有值，跳到引导页，并存储，下次打开就不会进去引导页
				uni.setStorage({
					key: 'launchFlag',
					data: true
				});
				console.log("去引导页");
				uni.redirectTo({
					url: '/pages/index/guide',
					success: (res) => {
						console.log("跳转引导页", res);
					}
				});
			}
		}

	}
</script>

<style>
</style>