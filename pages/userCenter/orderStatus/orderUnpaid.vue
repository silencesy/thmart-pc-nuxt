<template>
	<div class="user">
		<orderStatus flag="pay" type="1" :orderDetails="orderDetails">
			<div slot="statusInfo" class="statusInfo">
				<p>
					<span><img src="~/static/images/icon-yuandian.png" alt="">{{orderDetails.orderTime}}</span>
					<span>You have placed the order. Please make your payment within 15 minutes, or otherwise the order will be cancelled. </span>
				</p>
			</div>
		</orderStatus>
	</div>
</template>
<script>
	// 接口API
	import interfaceApi from '~/plugins/interfaceApi'
	import orderStatus from "~/components/user/orderStatus"
	export default {
		layout: 'userHome',
		middleware: 'userAuth',
		data() {
			return {
				
			}
		},
		async asyncData ({app,query}) {
        	console.log(query.orderNumber)
			let param = {
				orderNumber: query.orderNumber,
			}
		 	const orderDetails = await app.$axios.post(interfaceApi.OrderDetail,param);
  			return { 
  				orderDetails: orderDetails.data.data
  			}
		},
		components: {
			orderStatus
		},
		mounted() {

			
		},
	  	computed: {  
		    
	  	},
		methods: {

		}
	}
</script>

<style lang='sass' scoped>
	@import '~/assets/sass/common.sass'
	.user
		.statusInfo
			margin-left: 25px
			p 
				margin-bottom: 15px
				overflow: hidden 
				span 
					float: left
				span:first-child
					color: #666
					padding-right: 20px
					width: 193px
					line-height: 24px
					img 
						@include wh(13px, 13px)
						margin-right: 10px
					i.icon-dot
						color: #dfdfdf
						margin-right: 10px
						font-size: 13px
				span:nth-child(2)
					width: 500px
</style>
