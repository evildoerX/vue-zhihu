<template>
	<el-dialog  :title="cardInfoTitle" >
	  	<div class="cardinfocontent" v-html="cardInfoContent"> 
	  	</div>
  		<link rel="stylesheet" :href="cssUrl" /> 
	</el-dialog>
</template>
<script type="text/javascript"> 
	export default {
		name: "cardinfo",
		props: [   
			"cardInfoTitle",
			"cardInfoContent",
			"cssUrl"
		] 
	}
</script>
<style lang="scss">
	.headline{ 
		display: none; 
	}
</style>