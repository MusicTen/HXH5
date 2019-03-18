<template>
	<view class="index">
		<block v-for="(list, index) in lists" :key="index">
			<view class="row">
				<view class="card card-list2" v-for="(item,key) in list" @click="goDetail(item)" :key="key">
					<image class="card-img card-list2-img" :src="item.img_src"></image>
					<text class="card-num-view card-list2-num-view">{{item.img_num}}P</text>
					<view class="card-bottm row">
						<view class="car-title-view row">
							<text class="card-title card-list2-title">{{item.title}}</text>
						</view>
						<view @click.stop="share(item)" class="card-share-view"></view>
					</view>
				</view>
			</view>
		</block>
		<text class="loadMore">加载中...</text>
	</view>
</template>

<script>
	const $serverUrl = 'https://unidemo.dcloud.net.cn'
	export default {
		data() {
			return {
				refreshing: false,
				lists: [],
				fetchPageNum: 1
			}
		},
		onLoad() {
			this.getData();
			uni.getProvider({
				service: "share",
				success: (e) => {
					let data = [];
					for (let i = 0; i < e.provider.length; i++) {
						switch (e.provider[i]) {
							case 'weixin':
								data.push({
									name: '分享到微信好友',
									id: 'weixin'
								})
								data.push({
									name: '分享到微信朋友圈',
									id: 'weixin',
									type: 'WXSenceTimeline'
								})
								break;
							case 'qq':
								data.push({
									name: '分享到QQ',
									id: 'qq'
								})
								break;
							default:
								break;
						}
					}
					this.providerList = data;
				},
				fail: (e) => {
					console.log("获取登录通道失败", e);
				}
			});
		},
		onPullDownRefresh() {
			console.log("下拉刷新");
			this.refreshing = true;
			this.getData();
		},
		onReachBottom() {
			this.getData();
		},
		methods: {
			getData() {
				uni.request({
					url: $serverUrl + '/api/picture/posts.php?page=' + (this.refreshing ? 1 : this.fetchPageNum) + '&per_page=10',
					success: (ret) => {
						if (ret.statusCode !== 200) {
							console.log("请求失败:", ret)
						} else {
							if (this.refreshing && ret.data[0].id === this.lists[0][0].id) {
								uni.showToast({
									title: "已经最新",
									icon: "none",
								})
								this.refreshing = false;
								uni.stopPullDownRefresh()
								return;
							}
							let list = [],
								lists = [],
								data = ret.data;
							for (let i = 0, length = data.length; i < length; i++) {
								let index = Math.floor(i / 2);
								list.push(data[i]);
								if (i % 2 == 1) {
									lists.push(list);
									list = [];
								}
							}
							console.log("得到lists", lists);
							if (this.refreshing) {
								this.refreshing = false;
								uni.stopPullDownRefresh()
								this.lists = lists;
								this.fetchPageNum = 2;
							} else {
								this.lists = this.lists.concat(lists);
								this.fetchPageNum += 1;
							}
						}
					}
				});
			},
			goDetail(e) {
				uni.navigateTo({
					url:"./hotpic-detail?data=" + encodeURIComponent(JSON.stringify(e))
				})
			},
			share(e) {
				if (this.providerList.length === 0) {
					uni.showModal({
						title: "当前环境无分享渠道!",
						showCancel: false
					})
					return;
				}
				let itemList = this.providerList.map(function (value) {
					return value.name
				})
				uni.showActionSheet({
					itemList: itemList,
					success: (res) => {
						uni.share({
							provider: this.providerList[res.tapIndex].id,
							scene: this.providerList[res.tapIndex].type && this.providerList[res.tapIndex].type === 'WXSenceTimeline' ? 'WXSenceTimeline' : "WXSceneSession",
							type: 0,
							title: "uni-app模版",
							summary: e.title,
							imageUrl: e.img_src,
							href: "https://uniapp.dcloud.io",
							success: (res) => {
								console.log("success:" + JSON.stringify(res));
							},
							fail: (e) => {
								uni.showModal({
									content: e.errMsg,
									showCancel:false
								})
							}
						});
					}
				})
			}
		}
	}
</script>

<style>
	view {
	    display: flex;
	}
	@font-face {
		font-family: texticons;
		font-weight: normal;
		font-style: normal;
		src: url('https://at.alicdn.com/t/font_702773_g9f89om4v3j.ttf') format('truetype');
	}
	
	.index {
		flex: 1;
	    width: 750upx;
	    min-height: 100vh;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	
	.row {
		flex-direction: row;
	}
	
	.column {
		flex-direction: column;
	}
	
	.card {
		position: relative;
		width: 710upx;
		margin: 20upx 20upx 20upx 20upx;
		border-radius: 10upx;
		overflow: hidden;
		flex-direction: column;
		background-color: #FFFFFF;
	}
	
	.card-img {
		width: 710upx;
		height: 1065upx;
	}
	
	.card-num {
		color: #FFFFFF;
		font-size: 13px;
		text-align: center;
	}
	
	.card-num-view {
		background-color: #FF80AB;
	    line-height: 1;
	    display: inline-block;
		padding: 3px 6px;
	    color: #FFFFFF;
	    font-size: 12px;
	    text-align: center;
		justify-content: center;
	    align-items: center;
		border-radius: 15px;
		position: absolute;
		top: 20upx;
		right: 20upx;
	}
	
	.card-bottm {
		justify-content: center;
		align-items: center;
	}
	
	.card-share-view {
		justify-content: center;
		align-items: center;
		padding: 14upx 0;
		color: #FF80AB;
		margin: 20upx 20upx 20upx;
		font-size: 30upx;
		font-family: texticons;
	}
	
	.card-share-view:before {
		content: '\e62d';
	}
	
	.car-title-view {
		flex: 1;
		padding: 14upx 0upx 14upx 20upx;
	}
	
	.card-title {
		flex: 1;
		font-size: 30upx;
		text-align: left;
		color: #555555;
		text-overflow: ellipsis;
		lines: 2;
		display: -webkit-box;
		white-space: normal;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 2;
		overflow: hidden;
	}
	.card-list2 {
		width: 345upx;
		margin: 20upx 0 20upx 20upx;
	}
	
	.card-list2-img {
		width: 345upx;
		height: 517upx;
	}
	
	.card-list2-num-view {
		transform: scale(0.8);
	    transform-origin: right;
	}
	
	.card-list2-num {
		font-size: 22upx;
	}
	
	.card-list2-title {
		font-size: 26upx;
	}
	
	
	.loadMore {
		font-size: 30upx;
		color: #555;
		margin-bottom: 20upx;
	}
</style>
