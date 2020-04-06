<template>
	<view>
			<cu-custom bgColor="bg-yellow" isBack="true">
				<block slot="backText">返回</block>
				<block slot="content" >个人信息</block>
			</cu-custom>
			<!-- 头像 -->
			<view class="padding-sm flex" @tap="intoShenfenxinxi()">
				<text class="wenzi " style="margin-top: 50rpx;">头像</text>
				<view class="center  flex justify-end">
					<image class="head radius" style="margin-left: 10rpx;" :src="driverBasicInfo.user_zplj" ></image>
				</view>
				<!-- <image class="youjiantou" style="margin-top: 40rpx; margin-left: 20rpx;" src="/static/images/icon_right.png"></image> -->
			</view>
			<view style="height: 30rpx; background-color: #f7f6f5;"></view>
			<!-- 手机号 -->
			<view class="padding-sm flex ">
				<text class="wenzi ">手机号</text>
				<view class="center flex justify-end">
					<text class="text-center" style="margin-left: 10rpx;" v-if="driverBasicInfo.user_sjh!=null">{{driverBasicInfo.user_sjh}}</text>
				</view>
			</view>
			<!-- 姓名 -->
			<view class="padding-sm flex ">
				<text class="wenzi ">姓名</text>
				<view class="center flex justify-end" >
					<text class="text-center" style="margin-left: 10rpx;" v-if="driverBasicInfo.user_xm!=null">{{driverBasicInfo.user_xm}}</text>
				</view>
			</view>
			<!-- 身份信息 -->
			<view class="padding-sm flex ">
				<text class="wenzi">身份信息</text>
				<view @tap="intoShenfenxinxi()">
					<view class="center  flex justify-end">
						<text class="text-center" style="margin-left: 10rpx;" v-if="driverBasicInfo.user_sfzh!=null">{{driverBasicInfo.user_sfzh}}</text>
					</view>
				</view>
				<image class="youjiantou" style="margin-left: 20rpx;" src="/static/images/icon_right.png"></image>
			</view>
			<!-- 车辆信息 -->
			<view class="padding-sm flex " @tap="intoCheliangxinxi(hevicleBasicInfo.cl_id)">
				<text class="wenzi ">我的车辆</text>
				<view class="center flex justify-end" >
					<text class="text-center" style="margin-left: 10rpx;" v-if="hevicleBasicInfo.cl_cph!=null">{{hevicleBasicInfo.cl_cph}}</text>
				</view>
				<image class="youjiantou" style="margin-left: 20rpx;" src="/static/images/icon_right.png"></image>
			</view>
			
			<!-- 添加车辆 -->
			<view class="padding-sm flex " @tap="intotianjiacheliang(hevicleBasicInfo.cl_id)">
				<text class="wenzi ">添加车辆</text>
				<view class="center flex justify-end" >
					<text class="text-center" style="margin-left: 10rpx;" v-if="hevicleBasicInfo.cl_cph!=null">{{hevicleBasicInfo.cl_cph}}</text>
					</view>
					<image class="youjiantou" style="margin-left: 20rpx;" src="/static/images/icon_right.png"></image>
			</view>
			
			<view class="padding-sm flex " @tap="intotianjiasiji(driverBasicInfo.user_id)">
				<text class="wenzi ">添加司机</text>
				<view class="center flex justify-end" >
					<text class="text-center" style="margin-left: 10rpx;" v-if="driverBasicInfo.user_xm!=null">{{driverBasicInfo.user_xm}}</text>
					</view>
					<image class="youjiantou" style="margin-left: 20rpx;" src="/static/images/icon_right.png"></image>
			</view>
			
			
			<!-- 我的证件 -->
			<view class="padding-sm flex ">
				<text class="wenzi ">我的证件</text>
				<view class="center  flex justify-end" @tap="intoWodezhengjian()">
					<text class="text-center" style="margin-left: 10rpx;">驾驶证、行驶证</text>
				</view>
				<image class="youjiantou"  style="margin-left: 20rpx;" src="/static/images/icon_right.png"></image>
			</view>
			
			
		</view>
	</template>
	
	<script>
		import configCommon from '@/common/js/config_common.js'
		import utilCommon from '@/common/js/util_common.js'
		import storeCommon from '@/common/js/store_common.js'
		import requestCommon from '@/common/js/request_common.js'
		
		export default{
			data(){
				return{
					driverBasicInfo:{},
					hevicleBasicInfo:{}
				}
			},
			onLoad() {
				//获取司机的id号
				var driverID=storeCommon.getUserID()
				//获取司机的基本信息
				this.getDriverBasicInfo(driverID)
				//获取车辆基本信息
				this.getHevicleBasicInfo(driverID)
			},
			onShow() {
				//获取司机的id号
				var driverID=storeCommon.getUserID()
				//获取司机的基本信息
				this.getDriverBasicInfo(driverID)
				//获取车辆基本信息
				this.getHevicleBasicInfo(driverID)
			},
			methods:{
				/**
				 * 获取司机基本信息
				 */
				
				
				/**
				 * 获取车辆基本信息
				 */
				
				
				/**
				 * 进入身份信息页面
				 */
				intoShenfenxinxi:function(){
					uni.navigateTo({
						url:'/pages/driver/chezhu/shenfenxinxi'
					})
				},
				/**
				 * 进入车辆信息页面
				 */
				intoCheliangxinxi:function(hevicleid){
					//判断司机是否进行了实名认证
					
						uni.navigateTo({
							url:'/pages/driver/chezhu/cheliangxinxi?cl_id='+hevicleid
						})
					
					
				},
				/**
				 * 进入我的证件页面
				 */
				intoWodezhengjian:function(){
					
						uni.navigateTo({
							url:'/pages/driver/chezhu/wodezhengjian'
						})
					
					
				},
				intotianjiacheliang:function(){
					
						uni.navigateTo({
							url:'/pages/driver/chezhu/tianjiacheliang'
						})
					
					
				},
				intotianjiasiji:function(){
					
						uni.navigateTo({
							url:'/pages/driver/chezhu/tianjiasiji'
						})
					
					
				},
			}
		}
	</script>
	
	<style>
		.head {
			width: 120rpx;
			height: 100rpx;
			margin: 8rpx;
		}
		.youjiantou{
			height: 40rpx;
			width: 40rpx;
		}
		.wenzi{
			width: 150rpx;
		}
		.center{
			width: 500rpx;
		}
	</style>
	