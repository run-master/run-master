<template>
	<view class="container">
		<cu-custom bgColor="bg-yellow" isBack="true">
			<block slot="backText">返回</block>
			<block slot="content">添加信息</block>
		</cu-custom>

		<view class="bg-white supply-goods shadow">
			<view class="padding-sm">
				<view>
					<tui-list-cell :hover="false">
						<view class="tui-line-cell">
							<view class="tui-title" >添加手机号</view>
							<input placeholder-class="phcolor" class="tui-input" placeholder="请添加手机号" type="text" v-model="result.cl_sjh" />
						</view>

					</tui-list-cell>
				</view>



				<view class="flex">
					<view class="align-center padding-sm">
						<text style="font-size: 25upx;color: #262B3A;font-weight: 700;">车辆照片</text>
					</view>
					<view class="padding-sm justify-start" @tap="popup()">
						<image :src="imgFiles" style="width: 100upx;height: 100upx;" v-if="imgFiles != ''"></image>
						<view style="width: 400upx;color: #888;display: flex;justify-content: space-between;align-items: center; " v-else>
							请添加车辆照片<text class='cuIcon-right' style="color: #8799a3;font-size: 34upx;"></text>
						</view>
					</view>
				</view>
				
				<view class="flex">
					<view class="align-center padding-sm">
						<text style="font-size: 25upx;color: #262B3A;font-weight: 700;">车辆信息</text>
					</view>
					<view class="solid-bottom padding-sm justify-start" @tap="popup2()">
						<view style="color: #000000;font-weight: 700;width: 400upx;" v-if="vehicleSelection != ''">{{vehicleSelection}}</view>
						<view style="width: 400upx;color: #888; display: flex;justify-content: space-between;align-items: center;" v-else>
							请填写车辆信息<text class='cuIcon-right' style="color: #8799a3;font-size: 34upx;"></text>
						</view>
					</view>
				</view>



			</view>
		</view>
		
		
		<tui-bottom-popup :show="popupShow" @close="popup">
			<view class="selectGoodsInfo" style="height:1200upx; overflow: auto;">
				<view class="my_msg" v-if="showMsg">{{msg}}</view>
				<view class="selectTitle" style="height: 100upx;">
					<view class="my_close" @tap="popup">
						取消
					</view>
					<view class="my_nav">
						添加车辆照片
					</view>
					<view class="my_confirm">
						<view @tap="saveHevicleInfo()">确定</view>
					</view>
				</view>
				<view class="">
					<view class="my_hot">
						<view class="my_title">
							<text style="margin-left: 110rpx; font-size: 24rpx;">车辆正面照片</text>
						</view>
		
						<view class="my_hot_list">
								<image class="img" :src="cl_img" @tap="uploadHeviclePhoto()"></image>
						</view>
					</view>
		
					<view class="my_hot">
						<view class="my_title">
							<text style="margin-left: 80rpx; font-size: 24rpx;">行驶证正面照</text>
						</view>
							
						<view class="my_hot_list">
								<image class="img" :src="xsz_img" @tap="uploadHevicleLicenseFrontPhoto()"></image>
						</view>
					</view>
					
				</view>
			</view>
		</tui-bottom-popup>
		
		

		<!-- <view> -->
		<tui-bottom-popup :show="popupShow2" @close="popup2">
			<view class="selectGoodsInfo" style="height: 1200upx;overflow: auto">
				<view class="my_msg" v-if="showMsg2">{{msg2}}</view>
				<view class="selectTitle" style="height: 100upx;align-items: center;">
					<view class="my_close" @tap="popup2">
						取消
					</view>
					<view class="my_nav">
						添加车辆
					</view>
					<view class="my_confirm">
						<view @tap="confirm()">确定</view>
					</view>
				</view>

				<view class="my_hot">
					<view class="my_title">
						车辆颜色
					</view>
					<view class="my_hot_list">
						<view style="width: 160upx;" :class="item.selected==true?'active':''" v-for="(item,index) in car_plate_color"
						 :key="index" @tap="addActive(index)">
							{{item.clcpys}}
						</view>
					</view>
				</view>
				<view class="my_hot">
					<view class="my_title">
						车长
					</view>
					<view class="my_hot_list">
						<view style="width: 160upx;" :class="item.selected==true?'active':''" v-for="(item,index) in car_lengths" :key="index"
						 @tap="addActive1(index)">
							{{item.clcc}}
						</view>
					</view>
				</view>
				<view class="my_hot">
					<view class="my_title">
						车型
					</view>
					<view class="my_hot_list">
						<view style="width: 160upx;" :class="item.selected==true?'active':''" v-for="(item,index) in car_shapes" :key="index"
						 @tap="addActive2(index)">
							{{item.cllx}}
						</view>
					</view>
				</view>
				<view class="my_hot">
					<view class="my_title">
						载重
					</view>
					<view class="my_hot_list">
						<view style="width: 160upx;" :class="item.selected==true?'active':''" v-for="(item,index) in car_weights" :key="index"
						 @tap="addActive3(index)">
							{{item.clzz}}
						</view>
					</view>
				</view>
				<view class="my_hot">
					<view class="my_title">
						车辆品牌
					</view>
					<view class="my_hot_list">
						<view style="width: 160upx;" :class="item.selected==true?'active':''" v-for="(item,index) in car_pinpais" :key="index"
						 @tap="addActive4(index)">
							{{item.clpp}}
						</view>
					</view>
				</view>


				<view class="my_hot" style="display: flex;align-items: center;justify-content: space-between;">
					<view class="my_title">
						车辆车牌号
					</view>
					<view class="car_cp">
						<input style="width: 81%;height: 100%;" placeholder="请输入车牌号" v-model="result.cl_cph" type="text" />
					</view>
					<text style="width: 0.5%;"></text>
				</view>
				<!--toast提示-->

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
				jsz_img:'/static/images/jiashizheng.png',
				cl_img: '/static/images/shangchuantouxiang.png',
				xsz_img: '/static/images/shangchuantouxiang.png',
				upload_clzp_flag: 0,
				upload_xsz_flag: 0,
				upload_head_flag: 0,
				upload_idcardfront_flag: 0,
				upload_jsz_flag:0,
				
				user_xm: '',
				jsz_zh: '',
				jsz_zjcx: '',
				jsz_cclzrqsj: '',

				userName: '',
				userIDNum: '',
				userPhoneNum: '',
				usertype:"",
				cl_sjh: "",
				
				car_plate_color: [],
				car_lengths: [],
				car_shapes: [],
				car_weights: [],
				car_pinpais: [],
				cl_cph: "",
				
				driverBasicInfo: "",
				DriverLicenseInfo:"",
				hevicleBasicInfo: "",
				vehicleSelection: "",
				TabCur: 0,
				driverID: '',

				popupShow: false,
				popupShow2: false,
				popupShow3: false,
				popupShow4:false,
				showMsg: false,
				msg: "",
				showMsg2: false,
				msg2: "",
				showMsg3: false,
				msg3: "",
				showMsg4: false,
				msg4: "",
				
				
				selectList: [],
				intoPageUrl: '',
				//是否显示modal弹窗
				modalStatus: false,
				//弹窗modal显示的内容
				modalContext: '',
				//弹窗modal的按钮颜色
				modalButton: [{
					text: "确定",
				}],
				imgFiles: '',
				result: {
					cl_cph: "",
					cl_cpys: "",
					cl_cpys_bz: null,
					cl_cc: "",
					cl_cc_bz: null,
					cl_lx: "",
					cl_lx_bz: null,
					cl_zz: "",
					cl_zz_bz: null,
					cl_pp: "",
					cl_pp_bz: null,
					cl_img_url: ""
				},
				imgList: [],
				ok1: false,
				ok2: false,
				ok3: false,
				ok4: false,
				ok5: false,

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
			/* var driverID=storeCommon.getUserID()
			//获取司机的基本信息
			this.getDriverBasicInfo(driverID) */
			
			
			var temp1 = []
			var temp2 = []
			var temp3 = []
			var temp4 = []
			var temp5 = []
			var temp6 = []
			
			//获取所有司机姓名
			
			
			
			
			
			//获取车辆的车牌颜色
			setTimeout(()=>{
					var url=configCommon.server_root_url + '/freight/hevicle/plate/color/get'
				    requestCommon.getRequest(url).then(res=>{
						for (var i=0,len=res.data.rst.length;i<len;i++) {
							var temp={
								clcpys:"",
								selected:false,
								bz:""	
							}
							temp.clcpys=res.data.rst[i].cl_cpys
							temp.bz=res.data.rst[i].cl_cpys_bz
							temp1.push(temp)
						}
						this.car_plate_color=temp1
					},
					error=>{
						console.log(error)
					})
				
			},200)
			
			
			//获取车辆的车长
			
			setTimeout(()=>{
					var url=configCommon.server_root_url + '/freight/hevicle/length/get'
				    requestCommon.getRequest(url).then(res=>{
						for (var i=0,len=res.data.rst.length;i<len;i++) {
							var temp={
								clcc: "",
								selected: false,
								bz: ""	
							}
							temp.clcc = res.data.rst[i].cl_cc
							temp.bz = res.data.rst[i].cl_cc_bz
							temp2.push(temp)
						}
						this.car_lengths = temp2
					},
					error=>{
						console.log(error)
					})
				
			},200)
		
			//车型
			
			setTimeout(()=>{
					var url=configCommon.server_root_url + '/freight/hevicle/type/get'
				    requestCommon.getRequest(url).then(res=>{
						for (var i=0,len=res.data.rst.length;i<len;i++) {
							var temp={
								cllx: "",
								selected: false,
								bz: ""
							}
							temp.cllx = res.data.rst[i].cl_lx
							temp.bz = res.data.rst[i].cl_lx_bz
							temp3.push(temp)
						}
						this.car_shapes = temp3
					},
					error=>{
						console.log(error)
					})
				
			},200)
			
		
			//载重
			
			setTimeout(()=>{
					var url=configCommon.server_root_url + '/freight/hevicle/weight/get'
				    requestCommon.getRequest(url).then(res=>{
						for (var i=0,len=res.data.rst.length;i<len;i++) {
							var temp={
								clzz: "",
								selected: false,
								bz: ""
							}
							temp.clzz = res.data.rst[i].cl_zz
							temp.bz = res.data.rst[i].cl_zz_bz
							temp4.push(temp)
						}
						this.car_weights = temp4
					},
					error=>{
						console.log(error)
					})
				
			},200)
			
			
			//车辆品牌
			
			setTimeout(()=>{
					var url=configCommon.server_root_url + '/freight/hevicle/brand/get'
				    requestCommon.getRequest(url).then(res=>{
						for (var i=0,len=res.data.rst.length;i<len;i++) {
							var temp={
								clpp: "",
								selected: false,
								bz: ""
							}
							temp.clpp = res.data.rst[i].cl_pp
							temp.bz = res.data.rst[i].cl_pp_bz
							temp5.push(temp)
						}
						this.car_pinpais = temp5
					},
					error=>{
						console.log(error)
					})
				
			},200)
			
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
			intoshanchu(){
				
				
					uni.navigateTo({
						url:'/pages/driver/chezhu/shanchuxinxi'
					})
			},
			
			popup: function() {
				this.popupShow = !this.popupShow
			},

			popup2: function() {
				this.popupShow2 = !this.popupShow2
			},
			
			hidepopup(){
				this.popupShow = false
			},
			hidepopup2(){
				this.popupShow2 = false
			},
			
			
			 
		
		/**
		 * 上传车辆照片
		 */
		
			
		/**
		 * 上传行驶证照片
		 */
		
			
		/**
		 * 保存车辆照片
		 */
		
/* 选择车辆颜色 */
		
/* 选择车辆长度 */
		
/* 选择车型 */
		
/* 选择车辆载重 */
		
/* 选择车辆品牌 */
	
	//车牌号
	

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
		/* margin-left: -80upx; */
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
