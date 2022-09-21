<template>
	<view>
		<view class="header">
			<text>分类</text>
			<image src="../../static/images/search1.png" mode=""></image>
		</view>
		<view class="cate-box">
			<scroll-view scroll-y="true" class="left" :show-scrollbar="false">
				<view v-for="item,index in listData" :key="item.id" @click="selectItem(index)">
					<view :class="{'left-item':true, 'active': Idx == index}">
						{{ item.name }}
					</view>
				</view>
			</scroll-view>


			<view class="right">
				<view class="right-box">
					<view class="right-item" v-for="child in listData[Idx].labelList" :key="child.id">
						{{ child.name }}
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import { list } from '../../api/index.js'
	import { reactive, toRefs } from 'vue'
	export default {
		setup() {
			const data = reactive({
				listData: [],
				Idx: 0
			})
			list().then(res => {
				console.log(res);
				data.listData = res.data
			})
			const selectItem = (index) => {
				data.Idx = index
			}
			return {
				...toRefs(data),
				selectItem
			}
		}
	}
</script>

<style lang="scss">
	.header {
		height: 100rpx;
		background-color: #345dc2;
		color: white;
		font-size: 35rpx;
		line-height: 100rpx;
		text-align: center;
		font-weight: 600;
		position: relative;
		image {
			position: absolute;
			right: 10rpx;
			top: 23rpx;
			width: 55rpx;
			height: 50rpx;
		}
	}
	.active {
		color: #345dc2 !important;
	}

	.active::before {
		content: "";
		position: absolute;
		width: 6rpx;
		height: 50rpx;
		background-color: #345dc2;
		left: 0;
		top: 35%;
	}

	.cate-box {
		width: 100%;
		display: flex;

		.left {
			width: 26%;
			text-align: center;
			height: calc(100vh - 100rpx);
			background-color: #f8f9fb;

			.left-item {
				height: 140rpx;
				line-height: 140rpx;
				font-size: 30rpx;
				font-weight: 400;
				position: relative;
				color: #8c8c8c;
			}
		}

		.right {
			flex: 1;

			.right-box {
				width: 100%;
				padding: 5%;

				.right-item {
					display: inline-block;
					padding: 2px 8px;
					box-sizing: border-box;
					border-radius: 30rpx;
					border: 1px solid #bbb;
					margin: 10rpx;
					font-size: 30rpx;
				}
			}
		}
	}
</style>
