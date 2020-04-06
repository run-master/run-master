<template>
	<view>
		<cu-custom bgColor="bg-yellow" :isBack="true">
			<block slot="backText">返回</block>
			<block slot="content">删除信息</block>
		</cu-custom>
		<scroll-view scroll-x class="bg-white nav " style="position: fixed;z-index: 999;">
			<view class="bg-white nav text-center">
				<view class="cu-item flex-sub" :class="0==TabCur?'text-yellow cur':''" @tap="tabSelect" data-id="0">
					司机信息
				</view>
				<view class="cu-item flex-sub" :class="1==TabCur?'text-yellow cur':''" @tap="tabSelect" data-id="1">
					车辆信息
				</view>
			</view>
		</scroll-view>
		<view style="height: 70upx;"></view>
		<view class="cu-card article" :class="isCard?'no-card':''" style="bottom: 60upx;">
				<view class="flex" style="justify-content: space-between;" v-if="TabCur==0">
					<view class="cu-item shadow" v-for="(item,index) in driverBasicInfo" :key="index" v-if="driverBasicInfo!=null&&driverBasicInfo.length>0">
						<view class="content">
							<view style="display: flex;flex-direction: column;">
								<view class="flex" style="margin-top: 10rpx;">
									<image style="height: 150upx;width: 150upx;" :src="item.user_sfzlj" v-if="item.user_sfzlj!=null"></image>
									<image style="height: 150upx;width: 150upx;" src="/static/images/huowu.png" v-else></image>
								</view>
							</view>
							<view class="information" style="margin-top: 7upx; margin-left: 5upx;">
								<view class="xinxi">{{item.user_id}}</view>
								<view class="xinxi">{{item.user_xm}}，{{item.user_sjh}}</view>
								<view class="xinxi">{{item.user_type}}，{{item.jsz_zh}}</view>
							</view>
					
				</view>
				</view>
			</view>
			<view v-else>
				<view class="flex-direction">
					<view class="flex justify-center" style="margin-top: 300rpx;">
						<tui-tips :fixed="false" imgUrl="/static/images/img_nodata.png">暂无添加信息</tui-tips>
					</view>
				</view>
			</view>
		</view>
		<view style="height:90upx ;"></view>
		<view class="my_foot bg-blue" @tap="deleteMsg">
			删除信息
		</view>
	</view>
</template>

<script>
	import configCommon from "@/common/js/config_common.js"
	import storeCommon from '@/common/js/store_common.js'
	import utilCommon from '@/common/js/util_common.js'
	import requestCommon from '@/common/js/request_common.js'

	export default {
		data() {
			return {
				// 是否是card
				isCard: false,
				// 选项卡值
				TabCur: 0,
				scrollLeft: 0,
				// 货物list
				goodsList: [],
				
				driverBasicInfo:{},
				hevicleBasicInfo:{}
			}
		},
		onLoad() {
			var driverID=storeCommon.getUserID()
			//获取司机的基本信息
			this.getDriverBasicInfo(driverID)
			//获取车辆基本信息
			this.getHevicleBasicInfo(driverID)
		},
		mounted() {

		},
		methods: {
			tabSelect(e) {
				this.TabCur = e.currentTarget.dataset.id;
				this.goodsList=[]
				console.log("this.TabCur==" + this.TabCur)
				//全部货物
				//历史货物
				if (this.TabCur == 0) {
					this.getDriverBasicInfo()
					// this.getUserHistoryGoods()
				} else if (this.TabCur == 1) { //发货中
					this.getHevicleBasicInfo()
				} 
				this.scrollLeft = (e.currentTarget.dataset.id - 1) * 60

			},

			/**
			 * 获取司机基本信息
			 */
			
			/**
			 * 获取车辆基本信息
			 */
			
			
			
			/**
			 * @param {Object} hw_id
			 * 删除信息
			 */
			
	
			
			
		}
	}
</script>

<style>
	.biaoti {
		font-size: 38rpx;
	}

	.xinxi {
		font-size: 32rpx;
	}

	.title1 {
		/* font-size: 30upx; */
		font-weight: 900;
		color: #333333;
	}
	.my_foot{
		position: fixed;
		bottom:0;
		width: 100%;
		height: 90upx;
		display: flex;
		align-items: center;
		justify-content: center;
		border-top: 1px solid  #F0F0F0;
	}
</style>

