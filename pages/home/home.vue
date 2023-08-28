<template>
	<view class="page">
		<view class="homeHeader">
			<img src="../../static/homeHeader.png" style="width: 100%;">
		</view>
		<view class="homeBody">
			<view class="today">
				<text class="today-text">TODAY</text>
				<view class="custom-sentence">
					今日威海下雨，记得带伞哦~
				</view>
			</view>
			<view class="part-in">
				<view class="part-in-text">
					猜你想参加
				</view>
				<turns :data="data" @achieve="achieve"></turns>
			</view>
			<view class="campus-recommend">
				<view class="today-date">
				</view>
				<view class="recommend-part">
					...
				</view>
			</view>
		</view>
	</view>
</template>

<script setup>
	import turns from '../../components/pc-turns/pc-turns.vue'
	import {
		ref,
		reactive,
		onMounted,
		computed,
		watch
	} from 'vue'
	const data = reactive([
		{
			src:'https://cdn.pixabay.com/photo/2022/03/31/14/53/camp-7103189_1280.png',//活动的图片
			date:'2023-08-20',
			time:'9:00',
			title:'发布会',
			position:'G101',
			tag:'学术讲座',//活动所属分类
			id:'1',
			detail:'56656556',//活动的详细信息
			status:1,//活动的喜欢or不喜欢  默认为喜欢 1   不喜欢为0
			viewNum:0,//活动的浏览量
			authorSrc:'https://cdn.pixabay.com/photo/2021/07/22/11/25/rabbit-6485072_1280.jpg',//发布组织头像
			authorName:'HITwhLinker',//发布者名称
			like: false, // 默认没点赞
			likeCount: 26, // 点赞数量
		},{
			src:'https://cdn.pixabay.com/photo/2022/03/31/14/53/camp-7103189_1280.png',//活动的图片
			date:'2023-08-20',
			time:'9:00',
			title:'发布会',
			position:'G101',
			tag:'学术讲座',//活动所属分类
			id:'2',
			detail:'56656556',//活动的详细信息
			status:1,//活动的喜欢or不喜欢  默认为喜欢 1   不喜欢为0
			viewNum:0,//活动的浏览量
			authorSrc:'https://cdn.pixabay.com/photo/2021/07/22/11/25/rabbit-6485072_1280.jpg',//发布组织头像
			authorName:'HITwhLinker',//发布者名称
			like: false, // 默认没点赞
			likeCount: 26, // 点赞数量
		},{
			src:'https://cdn.pixabay.com/photo/2022/03/31/14/53/camp-7103189_1280.png',//活动的图片
			date:'2023-08-20',
			time:'9:00',
			title:'发布会',
			position:'G101',
			tag:'学术讲座',//活动所属分类
			id:'3',
			detail:'56656556',//活动的详细信息
			status:1,//活动的喜欢or不喜欢  默认为喜欢 1   不喜欢为0
			viewNum:0,//活动的浏览量
			authorSrc:'https://cdn.pixabay.com/photo/2021/07/22/11/25/rabbit-6485072_1280.jpg',//发布组织头像
			authorName:'HITwhLinker',//发布者名称
			like: false, // 默认没点赞
			likeCount: 26, // 点赞数量
		},{
			src:'https://cdn.pixabay.com/photo/2022/03/31/14/53/camp-7103189_1280.png',//活动的图片
			date:'2023-08-20',
			time:'9:00',
			title:'发布会',
			position:'G101',
			tag:'学术讲座',//活动所属分类
			id:'4',
			detail:'56656556',//活动的详细信息
			status:1,//活动的喜欢or不喜欢  默认为喜欢 1   不喜欢为0
			viewNum:0,//活动的浏览量
			authorSrc:'https://cdn.pixabay.com/photo/2021/07/22/11/25/rabbit-6485072_1280.jpg',//发布组织头像
			authorName:'HITwhLinker',//发布者名称
			like: false, // 默认没点赞
			likeCount: 26, // 点赞数量
		},{
			src:'https://cdn.pixabay.com/photo/2022/03/31/14/53/camp-7103189_1280.png',//活动的图片
			date:'2023-08-20',
			time:'9:00',
			title:'发布会',
			position:'G101',
			tag:'学术讲座',//活动所属分类
			id:'5',
			detail:'56656556',//活动的详细信息
			status:1,//活动的喜欢or不喜欢  默认为喜欢 1   不喜欢为0
			viewNum:0,//活动的浏览量
			authorSrc:'https://cdn.pixabay.com/photo/2021/07/22/11/25/rabbit-6485072_1280.jpg',//发布组织头像
			authorName:'HITwhLinker',//发布者名称
			like: false, // 默认没点赞
			likeCount: 26, // 点赞数量
		},{
			src:'https://cdn.pixabay.com/photo/2022/03/31/14/53/camp-7103189_1280.png',//活动的图片
			date:'2023-08-20',
			time:'9:00',
			title:'发布会',
			position:'G101',
			tag:'学术讲座',//活动所属分类
			id:'6',
			detail:'56656556',//活动的详细信息
			status:1,//活动的喜欢or不喜欢  默认为喜欢 1   不喜欢为0
			viewNum:0,//活动的浏览量
			authorSrc:'https://cdn.pixabay.com/photo/2021/07/22/11/25/rabbit-6485072_1280.jpg',//发布组织头像
			authorName:'HITwhLinker',//发布者名称
			like: false, // 默认没点赞
			likeCount: 26, // 点赞数量
		},{
			src:'https://cdn.pixabay.com/photo/2022/03/31/14/53/camp-7103189_1280.png',//活动的图片
			date:'2023-08-20',
			time:'9:00',
			title:'发布会',
			position:'G101',
			tag:'学术讲座',//活动所属分类
			id:'7',
			detail:'56656556',//活动的详细信息
			status:1,//活动的喜欢or不喜欢  默认为喜欢 1   不喜欢为0
			viewNum:0,//活动的浏览量
			authorSrc:'https://cdn.pixabay.com/photo/2021/07/22/11/25/rabbit-6485072_1280.jpg',//发布组织头像
			authorName:'HITwhLinker',//发布者名称
			like: false, // 默认没点赞
			likeCount: 26, // 点赞数量
		},{
			src:'https://cdn.pixabay.com/photo/2022/03/31/14/53/camp-7103189_1280.png',//活动的图片
			date:'2023-08-20',
			time:'9:00',
			title:'发布会',
			position:'G101',
			tag:'学术讲座',//活动所属分类
			id:'8',
			detail:'56656556',//活动的详细信息
			status:1,//活动的喜欢or不喜欢  默认为喜欢 1   不喜欢为0
			viewNum:0,//活动的浏览量
			authorSrc:'https://cdn.pixabay.com/photo/2021/07/22/11/25/rabbit-6485072_1280.jpg',//发布组织头像
			authorName:'HITwhLinker',//发布者名称
			like: false, // 默认没点赞
			likeCount: 26, // 点赞数量
		},
	])
	const achieve = (open) => {
		console.log(open);
		console.log('666');
	}
</script>

<style lang="scss">
	.homeBody {
		padding: 10rpx  40rpx  0 40rpx;
		.today {
			width: 90%;
			height: 200rpx;
			margin: 0 auto;
			margin-bottom: 20rpx;
			.today-text {
				display: flex;
				justify-content: center;
				padding-top: 20rpx;
				float: left;
				color: #fc9696;
				font-weight: 700;
				writing-mode: vertical-lr;
				text-orientation: upright;
			}
			.custom-sentence {
				display: inline-block;
				margin-left: 50rpx;
				width: 85%;
				height: 200rpx;
				color:#fff;
				line-height: 200rpx;
				padding-left: 30rpx;
				background: url(../../static/customSentence.jpg) no-repeat  ;
				background-size: 100% 100%;
				box-shadow: 2rpx 6rpx 8rpx 4rpx rgba(0, 0, 0, 0.2), 3rpx 8rpx 15rpx 2rpx rgba(0, 0, 0, 0.19);
				border-radius: 20rpx;
			}
		}
		.part-in-text {
			font-weight: 600;
			font-size: 50rpx;
			margin-bottom: 40rpx;
		}
		
		
	}
	

</style>
