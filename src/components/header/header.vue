<template>
	<div class="header">
		<div class="content-wrapper">
			<div class="avatar">
				<img width="64" height="64" :src="seller.avatar">
			</div>
			<div class="content">
				<div class="name">
					<span class="brand"></span>
					<span class="title">{{seller.name}}</span>
				</div>
				<div class="description">
					{{seller.description}}/{{seller.deliveryTime}}分钟送达
				</div>
				<div class="supports" v-if="seller.supports">
					<!-- 如果没有seller.supports,则不显示 -->
					<span class="icon" :class="classMap[seller.supports[0].type]"></span><!-- 动态设置icon -->
					<span class="text">{{seller.supports[0].description}}</span>
				</div>
			</div>
			<div v-if="seller.supports" class="supports-count" @click="showDetail">
				<span class="count">{{seller.supports.length}}个</span>
				<i class="icon-cart">></i>
			</div>
		</div>
		<div class="bulletiln-wrapper" @click="showDetail">
			<span class="title"></span><span class="bulletiln-content">
				{{seller.bulletin}}
			</span><span class="icon-cart">></span>
		</div>
		<div class="bg">
			<img :src="seller.avatar" width="100%" height="100%">
		</div>
		<div class="detail" v-show="detailShow">
			
		</div>
	</div>
</template>

<script type = "text/ecmascript-6">
	export default {
		props: {
			seller: {
				type: Object
			}
		},
		data() {
			return {
				detailShow: false
			};
		},
		methods: {
			showDetail() {
				this.detailShow = true;
			}
		},
		created() {
			this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']; // 通过数组将type映射为相应的字符串
		}
	};
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import "../../common/stylus/mixin.styl"
.header
	position: relative
	color: #fff
	background: rgba(7,17,27,0.5)
	overflow: hidden
	.content-wrapper
		padding: 24px 16px 18px 24px
		font-size: 0 // 消除两个行内元素中间的空白字符
		position: relative
		.avatar
			vertical-align: top
			display: inline-block
			img
				border-radius: 2px
		.content
			display: inline-block
			margin-left: 16px
			.name
				margin: 2px 0 8px 0
				.brand
					vertical-align: top  // 顶部对齐
					display: inline-block
					width: 30px
					height: 18px
					/* background-image url(./brand@2x.png) */
					bg-image('brand')
					background-size: 30px 18px
					background-repeat: no-repeat
				.title
					margin-left: 6px
					font-size: 16px
					font-weight: bold
					line-hight: 18px
			.description
				margin-bottom: 10px
				font-size: 12px
				line-height: 12px
			.supports
				.text
					line-height: 12px
					margin-left: 4px
					font-size: 10px
				.icon
					vertival-align: top
					display: inline-block
					width: 12px
					height:12px
					background-size: 12px 12px
					baakground-repeat: no-repeat
					&.decrease
						bg-image('decrease_1')
					&.discount
						bg-image('discount_1')
					&.guarantee
						bg-image('guarantee_1')
					&.invoice
						bg-image('invoice_1')
					&.special
						bg-image('special_1')
		.supports-count
			font-size: 10px
			line-height: 24px
			position: absolute
			right: 12px
			bottom: 18px
			padding: 0 8px
			height: 24px
			border-radius: 14px
			background-color: rgba(0,0,0,0.2 )
			.count
				vertical-align: top
				font-size: 10px
			.icon-cart
				font-size: 14px
				margin-left: 2px
				line-height: 24px
				font-style: normal
	.bulletiln-wrapper
		/*font-size: 0*/
		height: 28px
		line-height: 28px
		padding: 0px 22px 0 12px
		white-space: nowrap //设置文字隐藏的三个组合
		overflow: hidden
		text-overflow: ellipsis
		position: relative
		background: rgba(7,17,27,0.2)
		.icon-cart
				font-size: 14px
				margin-left: 2px
				line-height: 24px
				font-style: normal
				position: absolute
				right: 12px
				bottom: 0
		.title
			vertical-align: top
			margin-top: 8px
			width: 22px
			height: 12px
			background-size: 22px 12px
			background-repeat: no-repeat
			display: inline-block
			bg-image('bulletin')
		.bulletiln-content
			margin-left: 4px
			font-size: 10px
	.bg
		position: absolute
		top: 0
		bottom: 0
		z-index: -1
		width: 100%
		height: 100%
		filter: blur(10px)
	.detail
		position: fixed
		top: 0
		left: 0
		background: rgba(7,17,27,0.8)
		width: 100%
		height: 100%
		z-index: 100
		overflow: auto
</style>