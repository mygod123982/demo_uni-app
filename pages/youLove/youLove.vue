<template>
	<view>
		<!-- 图片盒子 -->
		<view class="imgbox">
			<u-image  src="/static/login_logo1.png" borderRadius="10" mode="widthFix"></u-image>
		</view>
		<!-- 登陆box -->
		<view class="loginBox">
			<u-form :model="loginForm" label-width="160">
				<u-form-item label="用户名"><u-input v-model.trim="loginForm.username"></u-input></u-form-item>
				<u-form-item label="用户密码" ><u-input v-model.trim="loginForm.password" type="password" :passwordIcon="true"></u-input></u-form-item>
				<u-form-item label="验证码">
					<u-input v-model="loginForm.verify"></u-input>
					<u-button type="success" size="mini" @click="getCode" slot="right">{{ tips }}</u-button>
				</u-form-item>
			</u-form>
			<u-button @tap="login" type="primary">登陆</u-button>
		</view>
		
		<!-- 弹窗相关 -->
		<u-toast ref="uToast"></u-toast>
		<u-verification-code :seconds="seconds" @end="end" @start="start" ref="uCode" @change="codeChange"></u-verification-code>
	</view>
</template>

<script>
	import md5Libs from "uview-ui/libs/function/md5";
export default {
	data() {
		return {
			txt: '',
			loginForm: {
				username: '',
				password: '',
				verify: ''
			},
			tips: '',
			// refCode: null,
			seconds: 10
		}
	},
	methods: {
		login() {
			console.log('登陆')
		},
		change() {
			console.log(123)
		},
		codeChange(text) {
			this.tips = text
		},
		getCode() {
			if (this.$refs.uCode.canGetCode) {
				// 模拟向后端请求验证码
				uni.showLoading({
					title: '正在获取验证码'
				})
				setTimeout(() => {
					uni.hideLoading()
					// 这里此提示会被this.start()方法中的提示覆盖
					this.$u.toast('验证码已发送')
					// 通知验证码组件内部开始倒计时
					this.$refs.uCode.start()
				}, 2000)
			} else {
				this.$u.toast('倒计时结束后再发送')
			}
		},
		end() {
			this.$u.toast('倒计时结束')
		},
		start() {
			this.$u.toast('倒计时开始')
		}
	},
	onPullDownRefresh() {
		setTimeout(()=>{
			uni.stopPullDownRefresh()
		},1000)
	}
}
</script>

<style lang="scss">
	
	.imgbox {
		width: 750upx;
		height: 555upx;
		padding: 30upx;
		
	}
	
	.loginBox {
		width: 700upx;
		margin: 10upx auto;
		padding: 30upx;
		border-radius: 10upx;
		border: 5upx dashed #A0CFFF;
	}
</style>
