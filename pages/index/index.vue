<template>
	<view class="container">
		<uni-card :is-shadow="false" is-full>
			<text class="uni-h6">这是一台神奇的打印机。</text>
			
		</uni-card>

		<uni-section title="Hi!" type="line">
			<view class="example">
				<button type="primary" @click="goto('printMsg')">打印新消息</button>
				<br>
				<button type="default" @click="goto('printCategory')">打印预设消息</button>
				
			</view>
		</uni-section>


	</view>
</template>

<script>
	export default {
		data() {},
		onLoad() {},
		onReady() {},
		methods: {
			goto(ref) {
				uni.navigateTo({
					url: '/pages/index/'+ref
				})
			},
		}
	}
</script>

<style lang="scss">
	.example {
		padding: 15px;
		background-color: #fff;
	}

	.segmented-control {
		margin-bottom: 15px;
	}

	.button-group {
		margin-top: 15px;
		display: flex;
		justify-content: space-around;
	}

	.form-item {
		display: flex;
		align-items: center;
		flex: 1;
	}

	.button {
		display: flex;
		align-items: center;
		height: 35px;
		line-height: 35px;
		margin-left: 10px;
	}
</style>
