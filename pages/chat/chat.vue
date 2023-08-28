<template>
	<view class="chat">
		<!-- 主要聊天页面 -->
		
		<scroll-view class="content" scroll-y="true" :scroll-into-view="`msg${msgs.length-1}`" :scroll-with-animation="true">
			<view class="msg-list">
				<view class="msg-item" :id="`msg${index}`" v-for="(msg, index) in msgs" :key="msg.time">
					<left-chat v-if="msg.left" :msg="msg" :head_img_url="left_avatar"></left-chat>
					<right-chat v-else :msg="msg" :head_img_url="right_avatar"></right-chat>
				</view>
			</view>
		</scroll-view>
		<view class="bottom-input">
			<text class="iconfont icon-yuyin icon"></text>
			<view class="textarea-container">
				<textarea auto-height :fixed="true" confirm-type="send" v-model="input" @confirm="submit" />
			</view>
			<text class="iconfont icon-luyin icon"></text>
			<text class="iconfont icon-jiahao icon"></text>
		</view>
	</view>
</template>

<script setup>
	import {
		ref,
		reactive
	} from 'vue'
	import {
		onLoad,
		onUnload
	} from '@dcloudio/uni-app'
import leftChat from '@/components/leftChat.vue'
import rightChat from '@/components/rightChat.vue'
<<<<<<< HEAD
	onLoad((obj) => {
		console.log(obj.name);
		uni.setNavigationBarTitle({
			title: obj.name
		})
	})
	const msgs = reactive([
		
=======

	let msgs = ref([
		// {
		// 	left: true,
		// 	content: "你好！",
		// 	tag:'text',
		// 	time: "2023/7/29 12:00:00"
		// }
>>>>>>> 9fac474502fa5a371ddff448135929c59706756d
	]);
	const udb = ref();
	let title = null;
	let server_id = null; // 内置表id
	let server_chat_id = null; // 聊天表id
	const scrollTop = ref(0)
	const input = ref("");
	let left_avatar = ref("");
	const right_avatar = ref("../../static/head.jpeg")
	const db = uniCloud.database();
	const myChatList = db.collection("server_chat_list"); // 聊天数据库
	const myCollection = db.collection('chat_list'); // 语料数据库
	let chats = null; // 所有问答对
	// const scrool_to_bottom = () => {
		
	// }
	const getAnswer = function(question) {
		for(var i=0;i<chats.length;i++) {
			if(chats[i].question_content === question) {
				return {
					content:chats[i].answer_content,
					tag:chats[i].answer_tag
				}
			}
		}
		
		return {
			content:"你好！",
			tag:"text"
		}
	}
	const updateChat = () => {
		// 更新最新信息
		const last_word = msgs.value[msgs.value.length-1]
		console.log(last_word);
		db.collection('server_list').doc(server_id).update({
			last_word:last_word.content,
			last_word_date:last_word.time
		})
		console.log("已更新");
		// .then((res) => {
		// 	console.log(udb);
		// 	udb.value.loadData();
		// })
	}
	const submit = function() {
		if (input.value === "") return;
		const inputValue = input.value
		input.value = ""
		msgs.value.push({
			left: false,
			content: inputValue,
			tag:"text",
			time: new Date().getTime(),
		});
<<<<<<< HEAD
		if(input.value === "你好，小助手，我喜欢街舞，你能给我推荐一下相关社团吗？") {
			const receiveText = "你好，以下是根据您的爱好：街舞，自动匹配到合适的社团： 凤舞社。						详细介绍：作为哈工大威海星级社团评选六连冠   hiphop（嘻哈舞）、popping（机械舞）、breaking（地板舞）、Locking（锁舞）、Jazz（爵士）、urban（编舞）、kpop（男女韩舞）！我们一个不少，任您选择。";
		}
		if(input.value === "这个社团训练时间是什么时候呀？") {
			const receiveText = "每周一到周四21：25--22:20 紧张学习的晚自习过后，欢迎来大活101室";
		}
		if(input.value === "最近学校有哪些讲座可以参加？") {
			const receiveText = "【光电·讲座】高能激光尾波加速和增强型固体高次谐波实验研究进展及激光等离子体不稳定性及其抑制研究                                                            主讲人：陈民、翁苏明   主办单位：理学院光电科学系 地点：主楼H124   时间：2023年7月31日上午8:30-11:30  "       
			}

		msgs.push({
			left: true,
			content: receiveText,
			time: new Date().getTime(),
		});
		input.value = "";
		last_item.value = 'msg' + (msgs.length - 1)
		console.log(msgs);
		console.log(last_item.value);
=======
		// 此处会有异步询问和错误处理
		setTimeout(()=>{
			const response = getAnswer(inputValue); // 获得回答，content 和 tag
			msgs.value.push({
				left: true,
				content: response.content,
				tag:response.tag,
				time: new Date().getTime(),
			});
			updateChat()
		}, 2000)
		
		// last_item.value = 'msg' + (msgs.length - 1)
>>>>>>> 9fac474502fa5a371ddff448135929c59706756d
	}
	// onLoad(res => {
	// 	uni.$on('listToChat',function(obj) {
	// 		left_avatar.value = obj
	// 		console.log(obj);
	// 	})
	// })
	
	const loadChat = () => {
		
		myChatList.get().then(res => {
			const data = res.result.data
						
			for(var i=0;i<data.length;i++) {
				if(data[i].name === title) {
					server_chat_id = data[i]._id;
					msgs.value = data[i].list;
				}
			}
		}).catch(error => {
			console.log(error);
		})
	}
	onLoad((obj) => {
		title = obj.name
		uni.setNavigationBarTitle({
			title: obj.name
		})
		left_avatar = obj.url;
		server_id = obj.id;
		loadChat() // 加载对话
		// 获取语料库
		myCollection.get().then(res => {
			chats = res.result.data
			// console.log(chats);
		}).catch(error => {
			console.log(error);
		})
	})
	onUnload(() => {
		// uni.$off('listToChat');
		// 更新聊天列表
		// myChatList.doc(server_chat_id).update({
		// 	list:msgs.value
		// })
	})
	
</script>

<style lang="scss" scoped>
	.chat {
		width: 100vw;
		height: calc(100vh - 44px);
		background-color: rgb(227,227,227);
	}
	.content {
		box-sizing: border-box;
		height: calc(90vh - 44px);
		padding: 0 10px;
	}
	.msg-list {
		margin-top: 20rpx;
	}
	.msg-item {
		margin-top: 10rpx;
	}
	.bottom-input {
		display: flex;
		align-items: flex-end;
		position: fixed;
		bottom: 0px;
		width: 100vw;
		min-height: 50px;
		background-color: $uni-bg-color-grey;
		padding: 10px;
		.textarea-container {
			flex-grow: 1;
			min-height: 30px;
			line-height: 30px;
			margin-left: 20rpx;
			background-color: #ffffff;
			textarea {
				width: calc(100vw - 146px);
				background-color: #ffffff;
			}
		}
		.icon {
			margin-left: 20rpx;
			font-size: 24px;
			// color: $uni-bg-color-grey;
		}
	}
</style>