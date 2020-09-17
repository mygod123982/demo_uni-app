<template>
	<view class="content">
		<view class="img-border"><image class="logo" src="/static/zmlogo.png" @click="open"></image></view>
		<view class="text-area">
			<text class="title">{{ list[pullrefreshNum] }}</text>
		</view>
		<uni-popup ref="popup" :animation="true" type="center">
			<uni-popup-dialog type="success" title="招聘启事" mode="base" @confirm="joinHell" content="你缺工作嘛?月薪0元起，工作随便选，点击确认加入我们"></uni-popup-dialog>
		</uni-popup>

		<uni-popup ref="successMsg" type="message">
			<uni-popup-message type="success" message="恭喜你抢到月薪0元工作一个,开始你的965生活吧" :duration="2000"></uni-popup-message>
		</uni-popup>
	</view>
</template>

<script>
import uniPopup from '@/components/uni-popup/uni-popup.vue'
import uniPopupMessage from '@/components/uni-popup/uni-popup-message.vue'
import uniPopupDialog from '@/components/uni-popup/uni-popup-dialog.vue'

export default {
	components: {
		uniPopup,
		uniPopupMessage,
		uniPopupDialog
	},
	data() {
		return {
			title: '上海朝明教育有限公司',
			list: ['上海朝明教育有限公司', '有着上海最伟大的教育团队', '工作认真，干活积极', '最主要的是不用花钱', '感动中国十大名企之一'],
			pullrefreshNum: 0
		}
	},
	onLoad() {},
	onPullDownRefresh() {
		if (this.pullrefreshNum >= this.list.length - 1) return uni.stopPullDownRefresh()
		this.pullrefreshNum++
		setTimeout(() => {
			uni.stopPullDownRefresh()
		}, 1000)
	},
	methods: {
		open() {
			this.$refs.popup.open()
		},

		joinHell(done) {
			this.$refs.successMsg.open()
			this.$refs.popup.close()
			done()
		}
	}
}
</script>

<style lang="scss">
.content {
	display: flex;
	position: relative;
	flex-direction: column;
	align-items: center;
	// height: calc(100vh - 44px);
	width: 100vw;
	/* justify-content: center; */
}

.logo {
	display: inline;
}

.img-border {
	border: 2px solid #007aff;
	border-radius: 10upx;
	height: 200rpx;
	width: 200rpx;
	margin-top: 200rpx;
	margin-left: auto;
	margin-right: auto;
	margin-bottom: 50rpx;
}

.text-area {
	display: flex;
	justify-content: center;
}

.title {
	font-size: 36rpx;
	color: #8f8f94;
	text-align: center;
}


</style>
