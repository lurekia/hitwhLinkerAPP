<template>
	<view class="chat">
		<!-- 头部 -->
		<view class="header">
			<text class="title">Student Buddy</text>
			<view class="tool">
				<text class="iconfont icon-tianjiahaoyou icon" @click="toContacts()"></text>
				<text class="iconfont icon-danlieliebiao icon" ></text>
			</view>
		</view>
		<!-- 所有好友列表 -->
		<!-- <scroll-view class="content" scroll-y="true"> 
			<ul>
				<li v-for="(chat, index) in chat_views" :key="index" class="chat-view" @click="handleClick(chat)">
					<image src="@/static/head.jpeg" mode="aspectFill" class="chat-img"></image>
					<view class="chat-content">
						<text class="text-name">{{chat.name}}</text>
						<text class="text-word">{{chat.last_word}}</text>
					</view>
					<view class="chat-date">
						<text>{{chat.last_word_date}}</text>
					</view>
				</li>
			</ul>
		</scroll-view> -->
		
		<scroll-view id="user-list-box" scroll-y="true">
			<!-- 会话用户列表 -->
			<uni-list :border="true">
				<uni-list-chat
				 v-for="(chat,index) in chatList" 
				 :key="chat.id"
				 :showBadge="chat.unread_count>0"
				 :badgeText="chat.unread_count"
				 :title="chat.title" 
				 :avatar="chat.avatar_file&&chat.avatar_file.url ? chat.avatar_file.url : '/uni_modules/uni-im/static/avatarUrl.png'" 
				 :note="chat.last_msg_note" 
				 :time="friendlyTime(chat.update_time)"
				 :clickable="true"
				 @click="handleClick(chat.id)"
				>
				</uni-list-chat>

			</uni-list>
		</scroll-view>
		
		
	</view>
</template>

<script setup>
<<<<<<< HEAD
import {reactive, ref} from 'vue'
<<<<<<< HEAD

const chat_views = reactive([
	
	{
		tag:"活动我先知",
		name:"活动我先知",
		head_img_url:"@/static/img3.jpg",
		last_word:"",
		last_word_date:""
	},
	{
		tag:"新生引导员",
		name:"新生引导员",
		head_img_url:"@/static/头像.jpeg",
		last_word:"",
		last_word_date:""
	},
	{
		tag:"餐厅探店侠",
		name:"餐厅探店侠",
		head_img_url:"@/static/img1.jpg",
		last_word:"",
		last_word_date:""
	},
	{
		tag:"预约助手",
		name:"预约助手",
		head_img_url:"@/static/img2.jpg",
		last_word:"",
		last_word_date:""
	},
	{
		tag:"学习助手",
		name:"学习助手",
		head_img_url:"@/static/img4.jpg",
		last_word:"",
		last_word_date:""
	},
]);

=======
import {
		onLoad
	} from '@dcloudio/uni-app'
let chat_views = reactive([]);
const udb = ref()
>>>>>>> 9fac474502fa5a371ddff448135929c59706756d
// 点击跳转聊天界面
const handleClick = (chat) => {
	console.log(chat);
	uni.navigateTo({
		url:`/pages/chat/chat?name=${chat.name}&url=${chat.avatar}&id=${chat._id}`, // 传递url感觉有点不好
=======
import {reactive, ref, computed} from 'vue'
import {
		onLoad
	} from '@dcloudio/uni-app'
import uniIm from '@/uni_modules/uni-im/lib/main.js';
import uniImUtils from '@/uni_modules/uni-im/common/utils.js';
import {
	store as uniIdStore,
	mutations as uniIdMutations
} from '@/uni_modules/uni-id-pages/common/store.js';

const db = uniCloud.database();

// 获取对话信息
let sortIndex = 0;
const chatList = computed(() => {
	sortIndex ++
	// console.log('根据会话时间排序',uniIm.conversation.dataList,sortIndex)
	let conversationList = uniIm.conversation.dataList
	setTimeout(()=> {
		sortIndex = 0
	}, 1000);
	if(sortIndex > 6){
		return conversationList
	}
	return conversationList.sort(function(a, b) {
		if(b.id == uniIm.currentConversationId) {
			// 当前会话正在输入时，不需要重新排序避免change频繁触发导致排序频繁 
			return 0
		}
		// 如果该会话的输入框已经输入了内容未发就排在前面
		if(b.chatText){
			b.update_time = Date.now()
		}
>>>>>>> 1f3e0e6725cd9f2f14e1664aeba701ecf80f60a0
		
		let a_update_time = a.update_time || 0
		let b_update_time = b.update_time || 0
		
		let aml = a.msgList.length
		let bml = b.msgList.length
		
		if (aml) {
			let create_time = a.msgList[aml - 1].create_time
			if (create_time > a_update_time) {
				a_update_time = create_time
			}
		}
		if (bml) {
			let create_time = b.msgList[bml - 1].create_time
			if (create_time > b_update_time) {
				b_update_time = create_time
			}
		}
		return b_update_time - a_update_time
	})
})
	// 加载更多
const loadMore = async function() {
	let data = await uniIm.conversation.loadMore()
	return data
}


// 点击跳转聊天界面
const handleClick = (chatId) => {
	console.log(chatId);
	uniIm.currentConversationId = chatId
	uni.navigateTo({
		url: '/uni_modules/uni-im/pages/chat/chat?conversation_id=' + chatId,
		animationDuration: 300
	})
	// uni.navigateTo({
	// 	url:`/pages/chat/chat?name=${chat.name}&url=${chat.avatar}&id=${chat._id}`, // 传递url感觉有点不好
		
	// })
	// console.log("传输信息给下一个");
	// uni.$emit('listToChat',chat.avatar)
}
// const formatDate = (time) => {
// 	const someDate = new Date(time);
// 	return someDate.toLocaleDateString();
// }
// const formatWord = (text) => {
// 	if(text.length <= 20) {
// 		return text;
// 	}
// 	else
// 		return text.slice(0,17) + "...";
// }

// 添加朋友

const toContacts = () => {
	uni.navigateTo({
		url:`/uni_modules/uni-im/pages/contacts/contacts`, 
	})
}

// 时间转换
const friendlyTime = (timestamp) => {
	return uniImUtils.toFriendlyTime(timestamp)
}
// onLoad(() => {
// 	const db = uniCloud.database();
// 	db.collection('server_list').get().then((res) => {
// 			chat_views = res.result.data
// 			console.log("获取用户信息:",chat_views);
// 		})
// 		.catch((error) => {
// 			console.log(error);
// 		})
// })
</script>

<style lang="scss" scoped>
.header {
	display: flex;
	justify-content: space-between;
	height: 10vh;
	line-height: 10vh;
	padding: 0 30rpx;
	border-bottom: 1px solid rgb(244, 244, 244);
	.title {
		font-size: 22px;
		font-weight: 600;
	}
	.tool {
		.icon {
			margin-left: 20rpx;
			font-size: 22px;
		}
		
	}
}
.content {
	height: calc(90vh - var(--window-bottom));
	width: 750rpx;
	ul {
		padding: 0;
	}
	ul li {
		box-sizing: border-box;
		list-style: none;
	}
	.chat-view {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		width: 100vw;
		height: 64px;
		padding: 3vw;
		border-bottom: 1px solid rgb(244, 244, 244);
		.chat-img {
			width: 10vw;
			height: 10vw;
		}
		.chat-content {
			display: flex;
			flex-direction: column;
			width: 65vw;
			.text-name {
				line-height: 22px;
				font-size: 16px;
			}
			.text-word {
				line-height: 22px;
				font-size: 13px;
				color: $uni-text-color-grey;
			}
		}
		.chat-date {
			width: 10vw;
			font-size: 12px;
			color: $uni-text-color-grey;
		}
	}
}

</style>
