<template>
	<view class="container">
		<uni-card :is-shadow="false" is-full>
			<text class="uni-h3 text-center">这是一台神奇的打印机。</text>
		</uni-card>

		<uni-section title="填写打印内容" type="line">
			<view class="example">
				<!-- 基础表单校验 -->
				<uni-forms ref="valiForm" :rules="rules" :model="valiFormData" labelWidth="120px" label-position="top">
					<uni-forms-item label="Code" required name="code">
						<uni-easyinput placeholder="请输入Code" />
					</uni-forms-item>
					<uni-forms-item label="打印内容" required name="printerCategory">
						<uni-data-select :localdata="printerCategoryRange" >
						</uni-data-select>
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
				printerCategoryRange: [],
				// 校验表单数据
				valiFormData: {
					code: '',
					printerCategory: ''
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
					printerCategory: {
						rules: [{
							required: true,
							errorMessage: '打印内容不能为空'
						}]
					}
				}
			}
		},
		onLoad() {
			uni.request({
				url:'http://printer.imluxin.com/api/printer/listCategory',
				success: (res) => {
						this.printerCategoryRange = res.data;
				    }
			})
		},
		onReady() {},
		methods: {
			submit(ref) {
				this.$refs[ref].validate().then(res => {
					console.log('success', res);
					// uni.showToast({
					// 	title: `校验通过`
					// });
					uni.request({
					    url: 'http://printer.imluxin.com/api/printer/printerCategory', //仅为示例，并非真实接口地址。
					    data: {
					        code: res.code,
							printerCategory: res.printerCategory
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
	.text {
    font-size: 36px;
    color: #666;
    margin-top: 5px;
  }
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
