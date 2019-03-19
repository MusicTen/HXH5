<template>
	<view>
		<view class="select-active" v-if="isselected" @tap="onchange">
			<view class="iconfont">&#xe69e;</view>
		</view>
		<view class="select" v-else @tap="onchange"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods: {
			onchange() {
				this.$emit('change');
			}
		},
		props: {
			isselected: {
				type: Boolean,
				default: false
			},
		},
	}
</script>

<style>
	@font-face {
		font-family: 'iconfont';  /* project id 1096241 */
		src: url('//at.alicdn.com/t/font_1096241_03iagh48h95q.eot');
		src: url('//at.alicdn.com/t/font_1096241_03iagh48h95q.eot?#iefix') format('embedded-opentype'),
		url('//at.alicdn.com/t/font_1096241_03iagh48h95q.woff2') format('woff2'),
		url('//at.alicdn.com/t/font_1096241_03iagh48h95q.woff') format('woff'),
		url('//at.alicdn.com/t/font_1096241_03iagh48h95q.ttf') format('truetype'),
		url('//at.alicdn.com/t/font_1096241_03iagh48h95q.svg#iconfont') format('svg');
	}
	.iconfont{
		font-family: "iconfont" !important;
		font-size: 16px;font-style:normal;
		-webkit-font-smoothing: antialiased;
		-webkit-text-stroke-width: 0.2px;
		-moz-osx-font-smoothing: grayscale;
	}
	.select{
		width: 31upx;
		height: 31upx;
		border: 1upx solid #CCC;
		margin-right: 20upx;
		border-radius: 50%;
	}
	.select-active{
		width: 31upx;
		height: 31upx;
		margin-right: 20upx;
		border-radius: 50%;
		border: 1upx solid transparent;
	}
	.select-active .img{
		display: block;
		width: 100%;
		height: 100%;
		border-radius: 4upx;
	}
	.iconfont {
		color: #ff6364;
	}
	.shoppingcar .bottom-jiesuan .info .select {
		display: inline-block;
		vertical-align: middle;
	}
</style>
