<template>
	<view>
			<cu-custom bgColor="bg-yellow" >
				<block slot="backText">返回</block>
				<block slot="content" >我的</block>
			</cu-custom>
			<!-- 头像、信息-->
			<view class="flex" style="background: rgba(0,0,0,0.7); color: white;" @tap="intoGenrenxinxi()">
				<image class="head radius" style="margin-left: 30rpx;" :src="driverBasicInfo.user_zplj" ></image>
				<view class="msg-box margin-left-xs">
					<view class="msg-item " v-if="driverBasicInfo.user_xm!=null">{{driverBasicInfo.user_xm}}</view>
					<view class="msg-item " v-else>{{driverBasicInfo.user_nc}}</view>
					<view class="msg-item" style="font-size: 10rpx;" v-if="heviclePlate!=null&&heviclePlate!=''">
						{{heviclePlate}}
					</view>
				</view>
			</view>
			<!-- 钱包 -->
			<view class="qianbao flex" style="background: rgba(0,0,0,0.7); width: 100%; color: white;">
				<!-- 余额显示 -->
				<view style="height: 38rpx;">
					钱包余额<br/>
					0.00元
				</view>
				<!-- 右箭头-->
				<image class="youjiantou" style="margin-top: 25rpx; margin-left: 20rpx;" src="/static/images/icon_right.png"></image>
			</view>
			<view style="height: 30rpx; background-color: #f7f6f5;"></view>
			
			<!-- 功能选项 -->
			<view v-for="(item,index) in box" :key="index">
				<view class="flex padding-sm solid-bottom"  @tap="rd(item.url_page)">
					<image class="tubiao" :src="item.url" ></image>
					<text style="width: 160rpx; margin-left: 10rpx;">{{item.text}}</text>
					<image class="youjiantou" style="margin-left: 460rpx;" src="/static/images/icon_right.png"></image>
				</view>
			</view>
			
		</view>
	</template>
	
	<script>
		import configCommon from '@/common/js/config_common.js'
		import storeCommon from '@/common/js/store_common.js'
		import utilCommon from '@/common/js/util_common.js'
		import requestCommon from '@/common/js/request_common.js'
		
		export default{
			data(){
				return{
					box:[
								{
									url:'/static/images/fahuolishi.png',
									text:'我的货物',
									url_page:'/pages/fabuhuoyuan/fahuo'
								},
								{
									url:'/static/images/wodeqiuzhu.png',
									text:'我的求助',
									url_page:'/pages/qiuzhu/wodeqiuzhu'
								},
								{
									url:'/static/images/wodeshequ.png',
									text:'我的社区',
									url_page:'/pages/shequ/wodeshequ'
								},
								// {
								// 	url:'/static/images/gongju.png',
								// 	text:'工具',
								// 	url_page:'/pages/driver/wode/gongju'
								// },
								{
									url:'/static/images/shezhi.png',
									text:'设置',
									url_page:'/pages/driver/wode/shezhi'
								},
							],
							//司机基本信息
							driverBasicInfo:{},
							//车牌号
							heviclePlate:''
						}
					},
			onLoad() {
			
			},
			onShow() {
				console.log("enter onShow...")
				//获取司机的编号
				var driverID=storeCommon.getUserID()
				console.log("driverID=="+driverID)
				//获取司机的基本信息
				this.getDriverBasicInfo(driverID)
				//获取司机车辆的车牌号
				this.getDriverHeviclePlate(driverID)
			},
			mounted() {
				console.log("enter mountedd...")
				//获取司机的编号
				var driverID=storeCommon.getUserID()
				console.log("driverID=="+driverID)
				//获取司机的基本信息
				this.getDriverBasicInfo(driverID)
				//获取司机车辆的车牌号
				this.getDriverHeviclePlate(driverID)
			},
			methods:{
				/**
				 * 点击进入个人信息页面
				 */
				intoGenrenxinxi:function(){
					uni.navigateTo({
						url:'/pages/driver/wode/gerenxinxi'
					})
				},
				
				//v-for点击进入各个页面函数
				rd(url){
					uni.navigateTo({
						url:url
					})
					console.log(url)
				},
				
				/**
				 * 获取司机个人信息
				 */
				getDriverBasicInfo:function(driverID){
					var _self=this
					console.log("enter getDriverBasicInfo......")
					console.log("driverID=="+driverID)
					//从后台获取司机的基本信息
					var url=configCommon.server_root_url+'/freight/driver/basic/info/get/'+driverID
					requestCommon.getRequest(url).then(res=>{
						console.log(res)
						//请求成功
						if(res.statusCode==200){
							if(res.data.statusCode==0){
								_self.driverBasicInfo=res.data.rst
								console.log(_self.driverBasicInfo)
							}else{
								utilCommon.showToastInfo(utilCommon.server_update)
							}
						}else{
							utilCommon.showToastInfo(utilCommon.server_updata)
						}
					},error=>{
						console.log(error)
					})
				},
				
				/**
				 * 获取司机车辆的车牌号
				 */
				getDriverHeviclePlate:function(driverID){
					var _self=this
					console.log("enter getDriverHeviclePlate....")
					console.log("driverID=="+driverID)
					//从后台获取司机车辆的车牌号
					var url=configCommon.server_root_url+'/freight/hevicle/plate/get/'+driverID
					requestCommon.getRequest(url).then(res=>{
						console.log(res)
						//请求成功
						if(res.statusCode==200){
							if(res.data.statusCode==0){
								_self.heviclePlate=res.data.rst.cl_cph
								console.log(_self.heviclePlate)
							}else{
								utilCommon.showToastInfo(utilCommon.server_update)
							}
						}else{
							utilCommon.showToastInfo(utilCommon.server_update)
						}
					},
					error=>{
						console.log(res)
					})
			
					
				},
				
				
			},
		}
		
	</script>
	
	<style>
		.head {
			width: 120rpx;
			height: 120rpx;
			margin: 8rpx;
		}
		.msg-item {
			width: 468upx;
			padding: 5rpx;
		}
		.msg-box {
			width: 470upx;
			margin-top: 20rpx;
		}
		.qianbao{
			width: 200rpx;
			height: 100rpx;
			padding-left: 40rpx;
		}
		.youjiantou{
			height: 40rpx;
			width: 40rpx;
		}
		.tubiao{
			height: 50rpx;
			width: 50rpx;
		}
	</style>
	