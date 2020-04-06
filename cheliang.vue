<template>
	<view>
			<cu-custom bgColor="bg-yellow" isBack="true">
				<block slot="backText">返回</block>
				<block slot="content">车辆信息</block>
			</cu-custom>
			<!-- 证件照片 -->
			<view>
				<!-- 照片 -->
				<view class="flex justify-center" style="height: 230rpx; margin-top: 30rpx;">
					<!-- 车辆照片 -->
					<view class="flex-direction justify-center">
						<image class="img" :src="cl_img" @tap="uploadHeviclePhoto()"></image><br />
						<text style="margin-left: 110rpx; font-size: 24rpx;">车辆正面照片</text>
					</view>
					<!-- 行驶证正面照 -->
					<view class="flex-direction justify-center">
						<image class="img" :src="xsz_img" @tap="uploadHevicleLicenseFrontPhoto()"></image><br />
						<text style="margin-left: 80rpx; font-size: 24rpx;">行驶证正面照</text>
					</view>
				</view>
			</view>
	
			<view class="padding-sm flex ">
				<view class="wenzi  ">
					<view class="duiqi">车牌号</view>
				</view>
				<view class="center flex justify-end ">
					<input type="text" class="solid" placeholder="车牌号码" style=" height: 54rpx; width: 250rpx;" v-model="cl_cph" @tap="showHeviclePlateInput" />
					<!-- <view class="solid" style=" height: 54rpx; width: 250rpx;">
					<keyboard @keyboard="keyboardChange" :show.sync="show" active-border="#0deafe" base-border="38f8f8f"></keyboard>
					</view> -->
				</view>
				<image class="youjiantou " src="/static/images/icon_right.png"></image>
			</view>
			<view class="padding-sm flex ">
				<view class="wenzi  ">
					<view class="duiqi">车牌颜色</view>
				</view>
				<view class="center flex justify-end " @tap="showHevicleInfoModal(1)">
					<view class="duiqi" v-if="cl_cpys!=null">{{cl_cpys}}</view>
				</view>
				<image class="youjiantou" src="/static/images/icon_right.png"></image>
			</view>
			<view class="padding-sm flex ">
				<view class="wenzi  ">
					<view class="duiqi">车长</view>
				</view>
				<view class="center flex justify-end " @tap="showHevicleInfoModal(2)">
					<view class="duiqi" v-if="cl_cc!=null">{{cl_cc}}
					</view>
				</view>
				<image class="youjiantou " src="/static/images/icon_right.png"></image>
			</view>
			<view class="padding-sm flex ">
				<view class="wenzi  ">
					<view class="duiqi">车型</view>
				</view>
				<view class="center flex justify-end " @tap="showHevicleInfoModal(3)">
					<view class="duiqi" v-if="cl_lx!=null">{{cl_lx}}
					</view>
				</view>
				<image class="youjiantou" src="/static/images/icon_right.png"></image>
			</view>
			<view class="padding-sm flex ">
				<view class="wenzi  ">
					<view class="duiqi">载重</view>
				</view>
				<view class="center flex justify-end " @tap="showHevicleInfoModal(4)">
					<view class="duiqi" v-if="cl_zz!=null">{{cl_zz}}
					</view>
				</view>
				<image class="youjiantou" src="/static/images/icon_right.png"></image>
			</view>
			<view class="padding-sm flex ">
				<view class="wenzi  ">
					<view class="duiqi">车辆品牌</view>
				</view>
				<view class="center flex justify-end " @tap="showHevicleInfoModal(5)">
					<view class="duiqi" v-if="cl_zz!=null">{{cl_pp}}
					</view>
				</view>
				<image class="youjiantou" src="/static/images/icon_right.png"></image>
			</view>
			<view class="flex justify-center margin-top">
				<button class="btn" @tap="saveHevicleInfo()">提交</button>
			</view>
	
			<!-- 显示阴影 -->
			<view class="mask-screen" @tap="hideModal" v-show="showModalStatus"></view>
			<!-- 显示车牌颜色选择-->
			<block v-if="xuanze==1">
				<view :animation="animationData" class="region-box" v-show="showModalStatus">
					<view class="region-txt" :class="[tabIndex==index?'active':'']" v-for="(item,index) in car_plate_color" :key="index"
					 :data-index="index" @tap.stop="getRegion">{{item.cl_cpys}}</view>
				</view>
			</block>
			<!-- 显示车长选择 -->
			<block v-if="xuanze==2">
				<view :animation="animationData" class="region-box" v-show="showModalStatus">
					<view class="region-txt" :class="[tabIndex==index?'active':'']" v-for="(item,index) in car_lengths" :key="index"
					 :data-index="index" @tap.stop="getRegion">{{item.cl_cc}}</view>
				</view>
			</block>
			<!-- 显示车型选择 -->
			<block v-if="xuanze==3">
				<view :animation="animationData" class="region-box" v-show="showModalStatus">
					<view class="region-txt" :class="[tabIndex==index?'active':'']" v-for="(item,index) in car_shapes" :key="index"
					 :data-index="index" @tap.stop="getRegion">{{item.cl_lx}}
					</view>
				</view>
			</block>
			<!-- 显示载重选择 -->
			<block v-if="xuanze==4">
				<view :animation="animationData" class="region-box" v-show="showModalStatus">
					<view class="region-txt" :class="[tabIndex==index?'active':'']" v-for="(item,index) in car_weights" :key="index"
					 :data-index="index" @tap.stop="getRegion">{{item.cl_zz}}</view>
				</view>
			</block>
			<!-- 显示车辆品牌选择 -->
			<block v-if="xuanze==5">
				<view :animation="animationData" class="region-box" v-show="showModalStatus">
					<view class="region-txt" :class="[tabIndex==index?'active':'']" v-for="(item,index) in car_pinpais" :key="index"
					 :data-index="index" @tap.stop="getRegion">{{item.cl_pp}}</view>
				</view>
			</block>
	
			<!--显示车辆车牌号输入-->
			<view class="mask-screen" @tap="hideInputHeviclePlateModal()" v-show="show"></view>
			<view :animation="animationData" class="region-box1" style="overflow: scroll;" v-show="show">
				<view :style="bgheight">
					<div class="column">
						<keyboard @keyboard="keyboardChange" :show.sync="show" active-border="#0deafe" base-border="38f8f8f"></keyboard>
					</div>
				</view>
			</view>
	
	
			<!--toast提示-->
			<tui-toast ref="toast"></tui-toast>
			<!--显示modal,单个确定按钮-->
			<tui-modal :show="modalStatus" @click="handleModalClick" @cancel="hideModal2" :content="modalContext" :button="modalButton"></tui-modal>
	
		</view>
	</template>
	
	<script>
		import configCommon from '@/common/js/config_common.js'
		import storeCommon from '@/common/js/store_common.js'
		import utilCommon from '@/common/js/util_common.js'
		import requestCommon from '@/common/js/request_common.js'
		import tuiDrawer from "@/components/drawer/drawer"
	
		import keyboard from "@/components/mpvue-keyboard/mpvue-keyboard.vue";
		import {
			obj2style
		} from "@/components/mpvue-keyboard/index.js";
		export default {
			components: {
				tuiDrawer,
				keyboard
			},
			data() {
				return {
					car_plate_color: [],
					car_lengths: [],
					car_shapes: [],
					car_weights: [],
					car_pinpais: [],
	
					cl_img: '/static/images/shangchuantouxiang.png',
					xsz_img: '/static/images/xingshizheng.png',
					cl_id: '',
					cl_cph: '',
					cl_cpysbz: 0,
					cl_cpys: '',
					cl_ccbz: 0,
					cl_cc: '',
					cl_lxbz: 0,
					cl_lx: '',
					cl_zzbz: 0,
					cl_zz: '',
					cl_ppbz: 0,
					cl_pp: '',
	
					upload_clzp_flag: 0,
					upload_xsz_flag: 0,
	
					showModalStatus: false,
					animationData: "",
					regionTxt: "不限",
					tabIndex: 26,
					xuanze: 0,
					xuanze_flag: 0,
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
					intoPageUrl: '',
					//显示车牌号输入框
					show: false,
					//显示车牌号键盘和输入框
					// showInputHeviclePlateStatus: false,
				}
			},
			onLoad(options) {
				console.log("cl_id==" + options.cl_id)
				this.cl_id = options.cl_id
				//获取车辆认证的标志
				var clrz = storeCommon.getLoginUserInfo().user_clrz
				//车辆认证了就获取车辆信息
				if (clrz == 1) {
					//根据车辆的id号获取车辆的信息
					this.getHevicleInfo(this.cl_id)
				}
				//获取车辆的车牌颜色
				this.getHeviclePlateColor()
				//获取车辆的车长
				this.getHevicleLength()
				//获取车辆车型
				this.getHevicleType()
				//获取车辆载重
				this.getHevicleWeight()
				//获取车辆品牌
				this.getHevicleBrand()
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
				/**
				 * 根据车辆的id号获取车辆的信息
				 */
				
	
				/**
				 * 输入车辆的车牌号
				 */
			
				/**
				 * 获取输入的车牌号
				 */
				
				/**
				 * 隐藏车牌号输入框弹窗
				 */
				
	
				/**
				 * 获取车辆的车牌颜色
				 */
				
				/**
				 * 获取车辆车长
				 */
				
				/**
				 * 获取车辆车型
				 */
				
				/**
				 * 显示车辆载重
				 */
				
				/**
				 * 显示车辆品牌
				 */
				
	
				/**
				 * 显示车辆信息弹窗
				 */
				
	
				/**
				 * 显示车牌颜色弹窗
				 */
				
				/**
				 * 弹窗显示车辆车长
				 */
				
				/**
				 * 显示车辆重量的弹窗
				 */
				
				/**
				 * 显示车辆品牌的弹窗
				 */
				
				/**
				 * 获取选择的内容
				 */
				
	
				/**
				 * 上传车辆照片
				 */
				
	
				/**
				 * 上传行驶证照片
				 */
				
				/**
				 * 保存车辆信息
				 */
				
	
				/**
				 * 显示弹窗
				 */
				
				/**
				 * @param {Object} e选择按钮
				 */
				
				/**
				 * 隐藏modal弹窗
				 */
				
	
			}
		}
	</script>
	
	<style>
		.img {
			width: 200rpx;
			height: 150rpx;
			margin-top: 25rpx;
			margin-left: 50rpx;
		}
	
		.wenzi {
			width: 150rpx;
			height: 54rpx;
		}
	
		.center {
			width: 500rpx;
			height: 54rpx;
		}
	
		.youjiantou {
			height: 50rpx;
			width: 40rpx;
			margin-top: 1rpx;
		}
	
		.duiqi {
			margin-top: 5rpx;
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
	
		/*底部抽屉样式 start*/
	
		.mask-screen {
			width: 100%;
			height: 100%;
			position: fixed;
			top: 0;
			left: 0;
			background: #000;
			opacity: 0.5;
			overflow: hidden;
			z-index: 9;
		}
	
		.region-box {
			width: 100%;
			overflow: hidden;
			position: fixed;
			bottom: 0;
			left: 0;
			z-index: 10;
			background: #fff;
			padding-top: 20upx;
			height: 670upx;
			padding: 40upx 30upx 48upx 30upx;
			box-sizing: border-box;
			display: flex;
			flex-direction: row;
			flex-wrap: wrap;
			align-items: flex-start;
			justify-content: flex-start;
			align-content: flex-start;
		}
	
		.region-txt {
			width: 150upx;
			height: 82upx;
			background: #e9edfc;
			line-height: 82upx;
			border-radius: 6upx;
			font-size: 28upx;
			color: #333;
			text-align: center;
			margin-right: 23upx;
			margin-bottom: 26upx;
			/* flex-grow: 1 */
		}
	
		.grow {
			flex-grow: 0
		}
	
		.active {
			background: #5677FC;
			color: #fff;
		}
	
		/*底部抽屉样式 end*/
		/*车牌号输入框样式*/
		.column {
			display: flex;
			display: -webkit-flex;
			flex-direction: column;
			-webkit-flex-direction: column;
		}
		
		/*底部抽屉样式 start*/
		.mask-screen {
			width: 100%;
			height: 100%;
			position: fixed;
			top: 0;
			left: 0;
			background: #000;
			opacity: 0.5;
			overflow: hidden;
			z-index: 9;
		}
		.region-box1 {
			width: 100%;
			overflow: hidden;
			position: fixed;
			bottom: 0;
			left: 0;
			z-index: 10;
			background: #fff;
			padding-top: 20upx;
			height: 750upx;
			/* padding: 40upx 30upx 48upx 30upx; */
			box-sizing: border-box;
			display: flex;
			flex-direction: row;
			flex-wrap: wrap;
			align-items: flex-start;
			justify-content: flex-start;
			align-content: flex-start;
		}
	</style>
	
