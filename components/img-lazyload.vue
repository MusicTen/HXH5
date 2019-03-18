<template>
	<view>
		<image :src="real_src"></image>
	</view>
</template>

<script>
	export default{
		name:img-lazyload,
		data(){
			return {
				real_src:"",
				placeholder_src:"",
			}
		},
		props:{
		},
		computed:{
		},
		methods:{
		}
	}
</script>

<style>
</style>
