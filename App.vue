<script>
	//1. 导入uni身份信息管理模块
	import uniIdPagesInit from '@/uni_modules/uni-id-pages/init.js';
	//2. 导入uniIm的Utils工具类
	import uniImUtils from '@/uni_modules/uni-im/common/utils.js';
	export default {
		onLaunch: async function() {
			console.log('App Launch')
			//3. 初始化uni身份信息管理模块
			uniIdPagesInit();
			//4. 初始化uniIm
			uniImUtils.init();
			console.log('初始化完毕');
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	
	@import url('http://at.alicdn.com/t/c/font_4171624_5f91t8g1imo.css');
	view {
		box-sizing: border-box;
	}
</style>
