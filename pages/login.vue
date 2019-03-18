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
					<input type="number" class="is-input1" maxlength="11" v-model="login.phone" placeholder="请输入手机号" @input="BindInput" data-val="phone" />
				</view>
				<view>
					<input class="is-input1" v-model="login.password" placeholder="请输入登录密码"  @input="BindInput" data-val="password"/>
				</view>

				<view class="loginbtn">
					<button :loading="login.loading" @tap="defaultHandlerLogin"> {{ login.loading ? "登录中...":"登 录"}} </button>
				</view>
				<view class="registerbtn">
					<button @tap="goRegister">注 册</button>
				</view>
			</view>
		</view>
		<view class="tips">
			<navigator url="#" hover-class="">
				<text>忘记密码？</text><text class="blue">点击找回</text>
			</navigator>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				login: {
					loading: false,
					phone: "",
					password: ""
				}
			};
		},
		methods:{
			defaultHandlerLogin:function(){
				this.login.loading = true;
				setTimeout((e=>{
					this.login.loading = false;
				}),1500);
				console.log(JSON.stringify(this.login)); 
			},
			goRegister () {
				uni.navigateTo({
					url: '/pages/register'
				});
			},
			BindInput:function(e){
				var dataval = e.currentTarget.dataset.val;
				this.login[dataval] = e.detail.value; 
			}
		}
	}
</script>
<style>
	.headimg {
		padding: 208rpx 0 20rpx;
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
	.registerbtn button,
	.loginbtn button {
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
	.registerbtn button {
		background: #999;
	}
	button:after {
		border: 2rpx solid #f2f2f2;
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
	.tips {
		padding: 40rpx 7% 0;
		text-align: right;
		font-size: 32rpx;
	}
	.blue {
		color: blue;
	}
</style>
