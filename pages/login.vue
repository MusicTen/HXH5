<template>
	<view>
		<view class="title">{{title}}</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '登录页'
			};
		},
		onLoad() {
			console.log('请登录')
		}
	}
</script>

<style>
	.title {
		font-size: 24px;
		color: red;
		text-align: center;
		}
</style>
