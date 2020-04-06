<template>
	<view class="bg-white">
			<cu-custom bgColor="bg-yellow" isBack="true">
				<block slot="backText">返回</block>
				<block slot="content">身份信息</block>
			</cu-custom>
			<!-- 上传头像 -->
			<view>
				<view class="flex justify-center">
					<text class="margin-left">请上传清晰的头像</text>
				</view>
				<view class="flex justify-center margin-top">
					<image class="shangchuantouxiang margin-top" :src="head_img" @tap="uploadHead()"></image>
					<view class="flex-direction margin-left">
						<view class="text-center">示例</view>
						<image class="shangchuantouxiang" :src="head_imgshili"></image>
					</view>
				</view>
			</view>
	
			<!-- 上传身份证正面照-->
			<view>
				<view class="flex justify-center margin-top">
					<text class="margin-left">请上传身份证正面照</text>
				</view>
				<view class="flex justify-center margin-top">
					<image class="shangchuantouxiang" :src="idcardfront_img" @tap="uploadIDCardFront()"></image>
					<view class="flex-direction margin-left">
						<view class="text-center">示例</view>
						<image class="shangchuantouxiang" :src="idcardfront_imgshili"></image>
					</view>
				</view>
			</view>
			
			<view>
				<tui-list-cell :hover="false">
					<view class="tui-line-cell">
						<view class="tui-title">输入姓名</view>
						<input placeholder-class="phcolor" class="tui-input" placeholder="请输入姓名" type="text" v-model="userName"/>
					</view>
				</tui-list-cell>
				
				<tui-list-cell :hover="false">
					<view class="tui-line-cell">
						<view class="tui-title">身份证号</view>
						<input placeholder-class="phcolor" class="tui-input" placeholder="请输入身份证号" type="text" v-model="userIDNum" maxlength="18"/>
					</view>
				</tui-list-cell>
				
				<tui-list-cell :hover="false">
					<view class="tui-line-cell">
						<view class="tui-title">手机号码</view>
						<input placeholder-class="phcolor" class="tui-input" placeholder="请输入手机号" type="number" v-model="userPhoneNum" maxlength="11" />
					
					</view>
				</tui-list-cell>
				
				<tui-list-cell :hover="false">
					<view class="tui-line-cell">
						<view class="tui-title">验证码</view>
						<input placeholder-class="phcolor" class="tui-input" placeholder="请输入验证码" type="number" v-model="userCode" maxlength="6"/>
						<button :style="bg_color" style=" width: 200rpx; height: 60rpx; font-size: 28rpx;" :disabled="disabled" @tap="getVarificationCode">{{title}}</button>
					</view>
				</tui-list-cell>
			</view>
			<view class="tui-btn-box">
				<button class="btn-primary" hover-class="btn-hover" formType="submit" type="primary" @tap="saveUserInfo()">提 交</button>
			</view>
			
			
			
			<!--toast提示-->
			<tui-toast ref="toast"></tui-toast>
			<!--显示modal,单个确定按钮-->
			<tui-modal :show="modalStatus" @click="handleModalClick" @cancel="hideModal" :content="modalContext" :button="modalButton"></tui-modal>
			
		</view>
	</template>
	
	<script>
		import configCommon from '@/common/js/config_common.js'
		import requestCommon from '@/common/js/request_common.js'
		import storeCommon from '@/common/js/store_common.js'
		import utilCommon from '@/common/js/util_common.js'
	
		import tuiListCell from "@/components/list-cell/list-cell"
		
		export default {
			components: {
				tuiListCell
			},
			data() {
				return {
					head_img: '/static/images/shangchuantouxiang.png',
					idcardfront_img: '/static/images/shangchuantouxiang.png',
					head_imgshili:'/static/images/touxiang.png',
					idcardfront_imgshili:'/static/images/shenfenzhengzhengmian.png',
					upload_head_flag: 0,
					upload_idcardfront_flag: 0,
					userName: '',
					userIDNum: '',
					userPhoneNum: '',
					userCode: '',
					timer: 60,
					title: '获取验证码',
					disabled: false,
					bg_color: 'background-color: #007AFF;',
					//临时电话号码
					tempPhone:'',
					//是否显示modal弹窗
					modalStatus: false,
					//弹窗modal显示的内容
					modalContext: '',
					//弹窗modal的按钮颜色
					modalButton: [{
						text: "确定",
						type: 'blue'
					}],
					//进入页面的url
					intoPageUrl: ''
				}
			},
			onLoad() {
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
			methods: {
				/**
				 * 根据用户的id号获取用户的照片和身份证正面照
				 */
				
				/**
				 * 上传头像照片
				 */
				
				/**
				 * 上传身份证正面照片
				 */
				
				/**
				 * 长传图片(比较两张照片是否是同一个人)
				 */
				
	
				/**
				 * 保存司机的照片和身份证来链接
				 */
				
	
				/**
				 * 获取验证码
				 */
				
				/*
				短信验证码，计时
				*/
				
				/**
				 * 保存用户信息
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
	
			}
		}
	</script>
	
	<style>
		.shangchuantouxiang {
			width: 200rpx;
			height: 200rpx;
		}
	
		.btn {
			width: 50%;
			height: 90rpx;
			line-height: 90rpx;
			background: linear-gradient(-90deg, #5677fc, #5c8dff);
			border-radius: 45rpx;
			color: #fff;
			font-size: 36rpx;
		}
	
		.frame {
			border: 0.5px solid #000000;
		}
	
		.wenzi {
			/* width: 150rpx; */
			width: 22%;
			height: 60rpx;
			text-align: center;
		}
	
		.input {
			height: 60rpx;
			/* width: 400rpx; */
			width: 65%;
		}
		
		/**输入框**********/
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
		
		.btn-gray {
			margin-top: 30rpx;
		}
	</style>
	