<template>
	<div> 
		<navigation></navigation>
		<div class="container"> 
		  	<el-carousel class="carousel-container " :interval="4000" type="card" height="288px">
			    <el-carousel-item v-for="item in banners">
			      	<img :src="item.url" :alt="item.title"/>
			    </el-carousel-item>
		  	</el-carousel>
		</div>
	  	<div class="container"> 
		  	<newcard class="newscard"  :listData="listDatas"></newcard>
		  	<el-button type="ghost" @click="getLatest">MNM</el-button>

	  	</div>
	</div>
</template>
<script>
	import navigation from "../components/navigation.vue"
	import newcard from "../components/newcard.vue"

	export default { 
 		components: {
			navigation,
			newcard 
		},
		data() {
			return {
				listDatas: [], 
				banners: [{
					title: "banner1",
					url: require("src/assets/banner/b_1.jpg") 
				},{
					title: "banner2",
					url: require("src/assets/banner/b_2.jpg") 
				},{
					title: " banner3",
					url: require("src/assets/banner/b_3.jpg")  
				},{
					title: "banner4",
					url: require("src/assets/banner/b_4.jpg") 
				},{
					title: "banner5",
					url: require("src/assets/banner/b_5.jpg")  
				},{
					title: "banner6",
					url: require("src/assets/banner/b_6.jpg")  
				}]
			}
		},
		created () {
			var vm = this;
			vm.getLatest();
		},
		methods: {
			getLatest: function(){
				var vm = this;
				// 详情页面
				// var url = "http://news-at.zhihu.com/api/4/news/9174415";
				var url = "http://news-at.zhihu.com/api/4/news/latest";
				vm.$http.jsonp("http://strun.club/source/phpJson/urljsonp.php",{
					params: {
						"love": "qin",
						"url": url
					}
				})
				.then(function(res){ 
					var result = JSON.parse(res.bodyText).stories;
					// console.log(JSON.parse(result));
					for (var i = 0 ; i < result.length ; i++) { 
						vm.listDatas.push(result[i])
					} 
				},function(res){})
			}
		}
	}
</script>
<style lang="scss" scoped>
	.el-carousel{ 
		.el-carousel__item{ 
		} 
	} 
	@media screen and (max-width: 992px){
		.carousel-container{
			display: none;
		}
	}  
</style> 