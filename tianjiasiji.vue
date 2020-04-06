<template>
	<view class="container">
		<cu-custom bgColor="bg-yellow" isBack="true">
			<block slot="backText">返回</block>
			<block slot="content">添加司机</block>
		</cu-custom>

		<view class="bg-white supply-goods shadow">
			<view class="padding-sm">
				<view class="flex">
					<view class="align-center padding-sm">
						<text style="font-size: 25upx;color: #262B3A;font-weight: 700;">添加司机</text>
					</view>
					<view class="solid-bottom padding-sm justify-start" @tap="popup">
						<view style="color: #000000;font-weight: 700;width: 400upx;" v-if="driverBasicInfo != ''">{{driverBasicInfo}}</view>
						<view style="width: 435upx;color: #888;display: flex;justify-content: space-between;align-items: center; " v-else>
							添加司机信息<text class='cuIcon-right' style="color: #8799a3;font-size: 34upx;"></text>
						</view>
					</view>
				</view>


				<view class="flex">
					<view class="align-center padding-sm">
						<text style="font-size: 25upx;color: #262B3A;font-weight: 700;">添加驾驶证</text>
					</view>
					<view class="solid-bottom padding-sm justify-start" @tap="popup2">
						<view style="color: #000000;font-weight: 700;width: 400upx;" v-if="DriverLicenseInfo!= ''">{{DriverLicenseInfo}}</view>
						<view style="width: 400upx;color: #888;display: flex;justify-content: space-between;align-items: center; " v-else>
							添加驾驶证信息<text class='cuIcon-right' style="color: #8799a3;font-size: 34upx;"></text>
						</view>
					</view>
				</view>
				</view>
				</view>

				<tui-bottom-popup :show="popupShow2" @close="popup2">
					<view class="selectGoodsInfo" style="height:1200upx; overflow: auto;">
						<view class="my_msg" v-if="showMsg2">{{msg2}}</view>
						<view class="selectTitle" style="height: 100upx;">
							<view class="my_close" @tap="popup2">
								取消
							</view>
							<view class="my_nav">
								添加驾驶证信息
							</view>
							<view class="my_confirm">
								<view @tap="saveDriverLicenseInfo()">确定</view>
							</view>
						</view>
						<view class="">
							<view class="my_hot">
								<view class="my_title">
									<text class="margin-top">上传驾驶证照片</text>
								</view>

								<view class="my_hot_list">
									<image class="shangchuantouxiang" :src="jsz_img" @tap="uploadDriverLicense()"></image>
								</view>
							</view>

							<view>
								<tui-list-cell :hover="false">
									<view class="tui-line-cell">
										<view class="tui-title">输入姓名</view>
										<input placeholder-class="phcolor" class="tui-input" placeholder="请输入姓名" type="text" v-model="user_xm" v-if="user_xm!=null" />
									</view>
								</tui-list-cell>

								<tui-list-cell :hover="false">
									<view class="tui-line-cell">
										<view class="tui-title">驾驶证号</view>
										<input placeholder-class="phcolor" class="tui-input" placeholder="请输入驾驶证号" type="text" v-model="jsz_zh" v-if="jsz_zh!=null" />
									</view>
								</tui-list-cell>

								<tui-list-cell :hover="false">
									<view class="tui-line-cell">
										<view class="tui-title">准驾车型</view>
										<input placeholder-class="phcolor" class="tui-input" placeholder="请输入准驾车型" type="text" v-model="jsz_zjcx"
										 v-if="jsz_zjcx!=null" />

									</view>
								</tui-list-cell>

								<tui-list-cell :hover="false">
									<view class="tui-line-cell">
										<view class="tui-title">初次领证日期</view>
										<input placeholder-class="phcolor" class="tui-input" placeholder="请输入初次领证日期" type="text" v-model="jsz_cclzrqsj"
										 v-if="jsz_cclzrqsj!=null" />
									</view>
								</tui-list-cell>
							</view>
						</view>
					</view>
				</tui-bottom-popup>



				<tui-bottom-popup :show="popupShow" @close="popup">
					<view class="selectGoodsInfo" style="height:1200upx; overflow: auto;">
						<view class="my_msg" v-if="showMsg">{{msg}}</view>
						<view class="selectTitle" style="height: 100upx;">
							<view class="my_close" @tap="popup">
								取消
							</view>
							<view class="my_nav">
								添加司机
							</view>
							<view class="my_confirm">
								<view @tap="saveUserInfo()">确定</view>
							</view>
						</view>
						<view class="">
							<view class="my_hot">
								<view class="my_title">
									<text class="margin-left">请上传清晰的头像</text>
								</view>

								<view class="my_hot_list">
									<image class="shangchuantouxiang margin-top" :src="head_img" @tap="uploadHead()"></image>
								</view>
							</view>

							<view class="my_hot">
								<view class="my_title">
									<text class="margin-left">请上传身份证正面照</text>
								</view>

								<view class="my_hot_list">
									<image class="shangchuantouxiang" :src="idcardfront_img" @tap="uploadIDCardFront()"></image>
								</view>
							</view>



							<view>
								<tui-list-cell :hover="false">
									<view class="tui-line-cell">
										<view class="tui-title">输入姓名</view>
										<input placeholder-class="phcolor" class="tui-input" placeholder="请输入姓名" type="text" v-model="userName" />
									</view>
								</tui-list-cell>

								<tui-list-cell :hover="false">
									<view class="tui-line-cell">
										<view class="tui-title">身份证号</view>
										<input placeholder-class="phcolor" class="tui-input" placeholder="请输入身份证号" type="text" v-model="userIDNum"
										 maxlength="18" />
									</view>
								</tui-list-cell>

								<tui-list-cell :hover="false">
									<view class="tui-line-cell">
										<view class="tui-title">手机号码</view>
										<input placeholder-class="phcolor" class="tui-input" placeholder="请输入手机号" type="number" v-model="userPhoneNum"
										 maxlength="11" />

									</view>
								</tui-list-cell>

								<tui-list-cell :hover="false">
									<view class="tui-line-cell">
										<view class="tui-title">驾驶身份</view>
										<input placeholder-class="phcolor" class="tui-input" placeholder="请输入驾驶身份:主驾驶/副驾驶" type="text" v-model="result.usertype"
										 maxlength="11" />
									</view>
								</tui-list-cell>


							</view>
						</view>
					</view>
				</tui-bottom-popup>
				<view class="my_foot bg-orange" @tap="intoshanchu()">保存</view>

				<!--toast提示-->
				<tui-toast ref="toast"></tui-toast>
				<!--显示modal,单个确定按钮-->
				<tui-modal :show="modalStatus" @click="handleModalClick" @cancel="hideModal" :content="modalContext" :button="modalButton"></tui-modal>
			</view>
</template>
<script>
	import configCommon from '@/common/js/config_common.js'
	import storeCommon from '@/common/js/store_common.js'
	import utilCommon from '@/common/js/util_common.js'
	import requestCommon from '@/common/js/request_common.js'
	import tuiSticky from '@/components/sticky';
	import tuiButton from '@/components/button';
	import tuiBottomPopup from "@/components/bottom-popup/bottom-popup"
	import tuiListCell from "@/components/list-cell/list-cell"

	var _this;
	export default {
		components: {
			tuiSticky,
			tuiButton,
			tuiBottomPopup,
			tuiListCell
		},
		data() {
			return {
				/* 	showModalStatus: false, */
				head_img: '/static/images/shangchuantouxiang.png',
				idcardfront_img: '/static/images/shangchuantouxiang.png',
				jsz_img: '/static/images/jiashizheng.png',
				upload_head_flag: 0,
				upload_idcardfront_flag: 0,
				upload_jsz_flag: 0,

				user_xm: '',
				jsz_zh: '',
				jsz_zjcx: '',
				jsz_cclzrqsj: '',

				userName: '',
				userIDNum: '',
				userPhoneNum: '',
				usertype: "",

				driverBasicInfo: "",
				DriverLicenseInfo: "",
				driverID: '',

				popupShow: false,
				popupShow2: false,
				showMsg: false,
				msg: "",
				showMsg2: false,
				msg2: "",

				intoPageUrl: '',
				//是否显示modal弹窗
				modalStatus: false,
				//弹窗modal显示的内容
				modalContext: '',
				//弹窗modal的按钮颜色
				modalButton: [{
					text: "确定",
				}],
				result: {
					
				},
				
			};
		},
		onLoad(options) {
			const that = this;

			uni.getSystemInfo({
				success: function(res) {
					that.winHeight = res.screenHeight
					console.log(that.winHeight)
				},

			})
			console.log(that.winHeight)
			//获取用户实名认证的标志
			var user_smrz = storeCommon.getUserIdentityFlag()
			console.log("user_smrz==" + user_smrz)
			//判断用户是否实名认证，若实名认证了就从后台获取钟照片和身份证正面照
			if (user_smrz == 1) {
				//获取用户的id号
				var driverID = storeCommon.getUserID()
				//根据用户的id号获取用户的基本信息
				this.getDriverBasicInfo(driverID)
			}
		},
		onShow() {

		},
		computed: {
			bgheight() {
				let style = {};
				const {
					screenHeight
				} = uni.getSystemInfoSync();
				style["height"] = screenHeight - uni.getStorageSync("CustomBar") + "px";
				return obj2style(style);
			}
		},
		methods: {
			//跳转页面，查看刚刚添加的信息
			intoshanchu() {


				uni.navigateTo({
					url: '/pages/driver/chezhu/shanchuxinxi'
				})
			},

			popup: function() {
				this.popupShow = !this.popupShow
			},

			popup2: function() {
				this.popupShow2 = !this.popupShow2
			},

			
			hidepopup() {
				this.popupShow = false
			},
			hidepopup2() {
				this.popupShow2 = false
			},
			
			/**
			 * 上传驾驶证
			 */
			
			/**
			 * 根据驾驶证照片获取驾驶证上的信息
			 */
			
			/**
			 * 保存驾驶证的信息
			 */
			

			/**
			 * 上传图片(比较两张照片是否是同一个人)
			 */
			
			/**
			 * 保存用户信息
			 */
			


			/**
			 * 上传头像照片
			 */
			
			/**
			 * 上传身份证正面照片
			 */
			
			/**
			 * 显示弹窗
			 */
			showModal() {
				this.modalStatus = true
			},
			/**
			 * @param {Object} e选择按钮
			 */
			handleModalClick(e) {
				let index = e.index;
				console.log("你点击的按钮index：" + index)
				this.hideModal()
			},
			/**
			 * 隐藏modal弹窗
			 */
			hideModal() {
				this.modalStatus = false
			},
},

}
</script>

<style>
	.active {
		border: 2px solid #f37b1d;
		color: #f37b1d;
	}

	.tips {
		font-size: 20upx;
	}

	.supply-goods {
		width: 90%;
		border-radius: 10px;
		margin-left: 5%;
		margin-top: 20px;
	}

	.selectGoodsInfo {
		border-top-left-radius: 20upx;
		border-top-right-radius: 20upx;
		display: flex;
		flex-flow: column;
		height: 1000upx;
		width: 100%;
		z-index: 999;
		background-color: #ffffff;
		color: #000000;
	}

	.selectGoodsInfo>.selectTitle {
		border-bottom: 1px solid #ccc;
		height: 9%;
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 10upx;

	}

	.my_confirm {
		height: 60upx;
		width: 120upx;
	}

	.my_confirm>view {
		background: #E56D00;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 25upx;
		margin-right: 20upx;
	}

	.my_close {
		margin-left: 20upx;
	}

	.my_nav {
		flex: 1;
		text-align: center;
		font-size: 40upx;
		font-weight: 700;
	}

	.my_foot {
		position: fixed;
		bottom: 0;
		width: 100%;
		height: 100upx;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.my_input {
		margin-top: 20upx;
		height: 85upx;
		width: 100%;
		background-color: #FFFFFF;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.my_input>view {
		width: 95%;
		height: 100%;
		background-color: #eee;
		font-size: 40upx;
		border-radius: 5px;
		display: flex;
		justify-content: space-between;
	}

	.my_input>view>text {
		line-height: 85upx;
		margin-left: 13upx;
	}

	.my_input>view>input {
		width: 90%;
		height: 100%;
		font-size: 30upx;
		border-radius: 5px;
	}

	.my_title {
		font-weight: 700;
	}

	.my_hot {
		margin-top: 20upx;
		margin-left: 20upx;
	}

	.my_hot>.car_cp {
		width: 500upx;
		height: 70upx;
		border-radius: 5px;
		background-color: #eee;
		display: flex;
		justify-content: center;
	}

	.my_hot>.car_cp>input {
		height: 70upx;
		width: 90%;
		background-color: #eee;
		border-radius: 5px;

	}


	.tui-title>input {
		height: 70upx;
		width: 90%;
		background-color: #eee;
		border-radius: 5px;

	}

	.my_hot_list {
		display: flex;
		flex-flow: wrap;

	}

	.my_hot_list>view {
		height: 70upx;
		padding-left: 25upx;
		padding-right: 25upx;
		display: flex;
		align-items: center;
		justify-content: center;
		background-color: #eee;
		margin-left: 20upx;
		margin-top: 20upx;
		border-radius: 5px;
	}

	.my_msg {
		position: fixed;
		top: 45%;
		width: 360upx;
		text-align: center;
		background: #ccc;
		padding-left: 40upx;
		padding-right: 40upx;
		padding-top: 30upx;
		padding-bottom: 30upx;
		left: 50%;
		margin-left: -180upx;
		border-radius: 40px;
	}

	.tui-line-cell {
		width: 100%;
		box-sizing: border-box;
		display: flex;
		align-items: center;
	}

	.tui-title {
		line-height: 32rpx;
		flex-shrink: 0;
	}

	.tui-input {
		font-size: 32rpx;
		color: #333;
		padding-left: 20rpx;
		flex: 1;
	}

	.tui-btn-box {
		padding: 40rpx 50rpx;
		box-sizing: border-box;
	}
</style>
