<template>
	<view>
		<view class="headimg">
			<view>
				<image src="../static/common/logo.jpg" mode="aspectFit" class="logoimg"></image>
			</view>
		</view>
		<view class="content">
			<view class="item">
				<view>
					<input type="number" maxlength="11" placeholder="请输入手机号" class="is-input1 " />
				</view>
				<view>
					<input type="number" maxlength="6" placeholder="短信验证码" class="is-input1 " />
					<view class="codeimg" @tap="getsmscode">{{smsbtn.text}}</view>
				</view>

				<view>
					<input placeholder="请输入登录密码" :password="true" class="is-input1" />

				</view>
				<view class="registerbtn">
					<button>注 册</button>
				</view>
			</view>
		</view>
		<view class="tips">
			<navigator url="#" hover-class="">
				<text>注册即表示同意</text><text class="blue">《用户协议》</text>
			</navigator>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				smsbtn: {
					text: '获取验证码',
					status: false,
					codeTime: 60
				},
				timerId: null
			};
		},
		methods: {
			getsmscode: function() {
				this.timerId = setInterval(() => {
						var codeTime = this.smsbtn.codeTime;
						codeTime--;
						this.smsbtn.codeTime = codeTime;
						this.smsbtn.text = codeTime + "S";
						if (codeTime < 1) {
							clearInterval(this.timerId);
							this.smsbtn.text = "重新获取";
							this.smsbtn.codeTime = 60;
							this.smsbtn.status = false;
						}
					},
					1000);
				return false;
			}
		}
	}
</script>

<style>
	.headimg {
		padding: 120rpx 0 20rpx;
	}
	.headimg > view {
		text-align: center;
	}
	.logoimg {
		width: 200rpx;
		height: 200rpx;
		border-radius: 50%;
		
	}
	.content {
		width: 85%;
		margin: 0 auto;
	}
	.item>view {
		margin-top: 20rpx;
	}


	.is-input1 {
		height: 88rpx;
		width: 100%;
		line-height: 88rpx;
		padding: 0 12rpx;
		color: #353535;
		font-size: 32rpx;
		box-sizing: border-box;
		appearance: none;
		border: 2rpx solid #e5e5e5;
		box-shadow: none;
		border-radius: 44rpx;
		outline: 0;
		display: block;
		padding-left: 30rpx;
		margin: 0;
		font-family: inherit;
		background: #fff;
		resize: none;
	}

	.iconfont {
		position: absolute;
		font-size: 40rpx;
		right: 12%;
		z-index: 999;
		width: 105rpx;
		text-align: center;
		color: #353535;
		margin-top: -11%;
		background: #fff;
		border-top-right-radius: 44rpx;
		border-bottom-right-radius: 44rpx;
		height: 80rpx;
		line-height: 80rpx;
	}

	.codeimg {
		position: absolute;
		font-size: 28rpx;
		right: 12%;
		z-index: 999;
		width: 200rpx;
		text-align: center;
		color: #353535;
		margin-top: -11%;
		background: #fff;
		border-top-right-radius: 44rpx;
		border-bottom-right-radius: 44rpx;
		height: 80rpx;
		line-height: 80rpx;
	}

	.registerbtn button {
		margin-top: 20rpx;
		height: 88rpx;
		width: 100%;
		line-height: 88rpx;
		color: #ffffff;
		font-size: 32rpx;
		border-radius: 44rpx;
		outline: 0;
		display: block;
		margin: 0;
		font-family: inherit;
		background: #ff6364;
		opacity: 0.8;
	}

	button:after {
		border: 2rpx solid #f2f2f2;
	}
	.tips {
		text-align: center;
		margin-top: 20rpx;
		font-size: 32rpx;
	}
	.blue {
		color: blue;
	}
</style>
