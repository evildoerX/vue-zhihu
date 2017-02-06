<template> 
	<!-- <el-card class="box-card">
	  	<div v-for="news in listData" class="text item">
	    	{{ news.title }}
	  	</div>
	</el-card> --> 
	<el-row class="box-card" :gutter="20"> 
		<el-col class="box-card-item":xs="24" :sm="12"  :md="8" v-for="news in listData" > 
		    <el-card :body-style="{ padding: '0px' }"> 
		      	<div style="padding: 14px;">
			        <h3>{{ news.title }}</h3>
			        <div class="card-body"></div>
			        <div class="card-bottom clearfix">
			          	<time class="time"><i class="el-icon-date"></i> {{ currentDate }}</time>
			          	<button :dataid="news.id" type="text" class="el-button el-button--text button" @click="newsInfoBtn"><i class="el-icon-d-arrow-right"></i> 查看详情</button>
			        </div>
		      	</div>
		    </el-card> 
		</el-col>
		<cardinfo ref="dv" :cardInfoTitle="cardTitle" :cardInfoContent="cardContent" :cssUrl="cssUrl"></cardinfo>
		 
	
		<div>
			<h1>vuex 测试</h1>
			Clicked: {{ getCount }} times
			<button @click="increment">+</button>
			<button @click="decrement">-</button>
		</div>
	</el-row>
</template>
<style lang="scss">
	.box-card{
		.box-card-item{
			margin-top: 18px;
			height: 120px;
			.el-card{
				position: relative;
				height: 100%;
			  	.card-bottom{
			  		position: absolute;
			  		bottom: 0;
			  		left: 0;
			  		right: 0; 
			  		padding: 10px 14px;
				    line-height: 1;
					.time {
					    font-size: 13px;
					    color: #999;
				  	}
				  	.button {
					    padding: 0 8px 0;
					    float: right;
					    width: auto;
				  	}
			  	}
			} 
		} 
	  	// .clearfix:before,
	  	// .clearfix:after {
	   //    	display: table;
	   //    	content: "";
	  	// }
		  
	  	// .clearfix:after {
	   //    	clear: both
	  	// } 
	  	.avatar,
	  	.content-image{
	  		display: none;
	  	} 
	}
</style>
<script>

	import cardinfo from "../components/cardinfo.vue"
	import {mapGetters} from 'vuex'
	import {mapActions} from 'vuex'
	export default {
		name: "newcard",
		props: [
			'listData' 
		],
 		components: { 
			cardinfo
		},
		computed: {
			// 使用对象展开运算符将 getters 混入 computed 对象中
			...mapGetters([
				'getCount' 
			])
		},
		data () { 
			return {
			 	currentDate: new Date(),
			 	storyId: "", 
				cardContent: " ",
				cardTitle: " ",
				cssUrl: "" 
			}
		},  
		methods: {
			...mapActions([
				'increment',
				'decrement', 
			]), 
			newsInfoBtn: function(event){
				var vm = this;
				var $ct = event.currentTarget.getAttribute("dataid");
				console.log($ct);
				let dom = vm.$refs.dv.$children[0];
				vm.$refs.dv.$children[0].open(); 
				vm.cardTitle = "正在加载内容..."; 
				vm.cardContent = "<div class='loading-container'><i class='fa fa-spinner fa-spin fa-3x fa-fw'></i><span class='sr-only'>Loading...</span><div>";
				var _url = "http://news-at.zhihu.com/api/4/news/";
				vm.$http.jsonp("http://strun.club/source/phpJson/urljsonp.php",{
					params:{
						"url": _url + $ct,
						"love": "qin"
					}
				}).then(function(res){  
					let result = JSON.parse(res.bodyText);
					console.log("****");
					vm.cardContent = result.body;
					vm.cardTitle = result.title;
					vm.cssUrl = result.css; 
					console.log("..."); 
				},function(res){}) 
			}
		} 

	}
</script>
