<template>
	<view class="container">
		<view class="cropper-wrap"><cropper id="image-cropper" ref="cropper" @cropped="cropped" :zoom="1" :angle="0" :max-zoom="3" :min-zoom="0.5" :src="src" :preSrc="preSrc" /></view>
		<view class="ctrls-wrap" @click="selectImg"><view class="ctrl">上传图片</view></view>
		<view class="ctrls-wrap" @click="selectPreImg"><view class="ctrl">上传前置图片</view></view>
		<view class="ctrls-wrap" @click="cutImg"><view class="ctrl">保存图片</view></view>
		<image :src="img" mode="aspectFit" />
	</view>
</template>
<script>
// import ImageCropper from '@/components/kd/uniapp-nice-cropper/src/cropper.vue';
// import ImageCropper from '@/components/kd/cropper/cropper.vue'

export default {
	data() {
		return {
			src: '',
			preSrc: '',
			img: ''
		};
	},
	methods: {
		cropped(e) {
			console.log(e);
			this.img = e;
		},
		errHandle(e) {
			console.log('图片加载失败了');
		},
		cutImg() {
			this.$refs.cropper.cutImg();
		},
		selectImg() {
			console.log("selectImg");
			uni.chooseImage({
				count: 1,
				sizeType: ['original'],
				sourceType: ['album', 'camera'],
				success: res => {
					var tempFilePaths = res.tempFilePaths;
					this.src = tempFilePaths[0];
				}
			});
		},
		selectPreImg() {
			console.log("selectPreImg");
			uni.chooseImage({
				count: 1,
				sizeType: ['original'],
				sourceType: ['album', 'camera'],
				success: res => {
					var tempFilePaths = res.tempFilePaths;
					this.preSrc = tempFilePaths[0];
				}
			});
		}
	}
};
</script>
<style>
page {
	height: 100%;
	overflow: hidden;
	background: #000;
	/* #ifdef MP-ALIPAY */
	position: absolute;
	width: 100%;
	/* #endif */
}
</style>
<style lang="scss" scoped>
.container {
	width: 100%;
	height: 100%;
	display: flex;
	flex-direction: column;
	& .cropper-wrap {
		// flex: 1;
		height: 50%;
	}
	& .ctrls-wrap {
		display: flex;
		justify-content: center;
		align-items: center;
		color: white;
		font-size: 34rpx;
		text-align: center;
		border-bottom: 1px solid #fff;
		height: 96rpx;
		& .ctrl {
			flex: 1;
		}
	}
}
</style>
