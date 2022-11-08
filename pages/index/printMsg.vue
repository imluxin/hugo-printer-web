<template>
	<view class="container">
		<uni-card :is-shadow="false" is-full>
			<text class="uni-h3 text-center">这是一台神奇的打印机。</text>
		</uni-card>

		<uni-section title="填写打印内容" type="line">
			<view class="example">
				<!-- 基础表单校验 -->
				<uni-forms ref="valiForm" :rules="rules" :model="valiFormData" labelWidth="80px" label-position="top" class="uni-h2" label-style="{'font-size':'20px'}">
					<uni-forms-item label="Code" required name="code" class="ulist-font-20">
						<uni-easyinput v-model="valiFormData.code" placeholder="请输入Code" />
					</uni-forms-item>
					<uni-forms-item label="标题" required name="title" class="ulist-font-20">
						<uni-easyinput type="textarea" class="uni-h2" v-model="valiFormData.title" placeholder="请输入标题" />
					</uni-forms-item>
					<uni-forms-item label="打印内容" name="content" class="ulist-font-20">
						<uni-easyinput type="textarea" v-model="valiFormData.content" placeholder="请输入打印内容" />
					</uni-forms-item>
				</uni-forms>
				<button type="primary" @click="submit('valiForm')">提交</button>
			</view>
		</uni-section>


	</view>
</template>

<script>
	export default {
		data() {
			return {
				printerCategoryRange: [
					{
						value: 1,
						text: "三年级诗词"
					}
				],
				// 校验表单数据
				valiFormData: {
					code: '',
					content: '',
					title: ''
				},
				// 校验规则
				rules: {
					code: {
						rules: [{
							required: true,
							errorMessage: 'code 不能为空'
						}, {
							format: 'number',
							errorMessage: 'code 只能输入数字'
						}]
					},
					title: {
						rules: [{
							required: true,
							errorMessage: '标题不能为空'
						}]
					}
				}
			}
		},
		onLoad() {},
		onReady() {},
		methods: {
			submit(ref) {
				this.$refs[ref].validate().then(res => {
					console.log('success', res);
					// uni.showToast({
					// 	title: `校验通过`
					// });
					uni.request({
					    url: 'http://printer.imluxin.com/api/printer/print', //仅为示例，并非真实接口地址。
					    data: {
					        code: res.code,
							title: res.title,
							content: res.content
					    },
						method:'POST',
					    success: (res) => {
					        console.log(res.data);
							console.log('code', res.data.msg);
							if(res.data.code == 201) {
								console.log(res.data.msg);
								uni.showModal({
									title: res.data.msg,
									showCancel: false,
									confirmColor: '#ff4e00',
									success: function (res) {
										if (res.confirm) {
											console.log('用户点击确定');
										} else if (res.cancel) {
											console.log('用户点击取消');
										}
									}
								});
							} else {
								uni.showModal({
									title: res.data.msg,
									showCancel: false,
									success: function (res) {
										if (res.confirm) {
											console.log('用户点击确定');
										} else if (res.cancel) {
											console.log('用户点击取消');
										}
									}
								});
							}
					    }
					});
				}).catch(err => {
					console.log('err', err);
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
	.text-center {
		text-align: center;
		display: block;
	}
</style>
