<template>
	<view class="container">
		<uni-card :is-shadow="false" is-full>
			<text class="uni-h3 text-center">这是一台神奇的打印机。</text>
		</uni-card>
		
		<uni-section title="选择功能" type="line">
			<uni-list>
				<uni-list-item title="打印新消息" note="" link to="/pages/index/printMsg" class="ulist-font-20" thumb="https://files.catbox.moe/gr4l34.png" thumb-size="lg" >
					
					<!-- <template v-slot:body>
							<text class="slot-box slot-text uni-h4">打印新消息</text>
					</template> -->
				</uni-list-item>
				<uni-list-item title="打印预设消息" note="" link to="/pages/index/printCategory" class="ulist-font-20" thumb="https://files.catbox.moe/4bofz6.png" thumb-size="lg" ></uni-list-item>
			</uni-list>
		</uni-section>

	</view>
</template>

<script>
	export default {
		data() {},
		onLoad() {},
		onReady() {},
		methods: {}
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
	.text-center {
		text-align: center;
		display: block;
	}
	.u-font-3 {
		font-size: 48px;
	}
</style>
