<template>
	<div>
		<div>
			<mt-header fixed  :title="onedata.title">
				<div slot="left" @click="backa()">
			    <mt-button icon="back"></mt-button>
			  </div>
			  
			</mt-header>
			
		</div>
		<div class="banner">
			<mt-swipe :auto="4000" :show-indicators="false">	
						<mt-swipe-item v-for="item in onedata.photo" :key="item.id">
						  <img :src="item" alt="">
						</mt-swipe-item>		
			</mt-swipe>
		</div>
		<div>
			<p>{{onedata.title}}</p>
			<p>{{onedata.directors}}</p>
			<p><img width="100%" :src="onedata.poster" alt=""></p>
			<p>{{onedata.info}}</p>
			<p><img width="100%" :src="onedata.detailcover" alt=""></p>
			<div>
				{{onedata.officialstory}}
			</div>
			
			<p>{{onedata.charge_edt}}{{onedata.editor_email}}</p>
		</div>
		<div class="pl">
			<p class="p1"><span>评论</span></p>
			<div v-for="itm in onedatapl.data" class="pla">
				<p><span><img width="30" :src="itm.user.web_url" alt=""></span><span>{{itm.user.user_name}}</span><span>{{itm.input_date}}</span></p>
				<div v-if='itm.touser' class="hf">
					<p><span><img width="30" :src="itm.touser.web_url" alt=""></span><span>{{itm.touser.user_name}}</span></p>
				     <p>{{itm.quote}}</p>
				</div>
				<p>{{itm.content}}</p>
			</div>
			
			
		</div>
	</div>
</template>
<script>
	
	import Vue from 'vue'
	import axios from 'axios'
	export default {
	  name: 'movexx',
	  data () {
	    return {
	      onedata:'',
	      item_id:'',
	      onedatapl:''
	     
	    }
	  },
	  methods:{
	  	shujua(){
	  		axios({
			  method:'get',
			  url: 'http://v3.wufazhuce.com:8000/api/movie/detail/ '+ this.item_id +' ?channel=wdj&source=channel_movie&source_id=9240&version=4.0.2&uuid=ffffffff-a90e-706a-63f7-ccf973aae5ee&platform=android'
			})
			.then(response => {
				this.onedata=response.data.data;
				
			})

	  	},
	  	
	  	shujub(){
	  		axios({
			  method:'get',
			  url: 'http://v3.wufazhuce.com:8000/api/comment/praiseandtime/movie/ '+ this.item_id + '/0?channel=wdj&version=4.0.2&uuid=ffffffff-a90e-706a-63f7-ccf973aae5ee&platform=android'
			})
			.then(response => {
				this.onedatapl=response.data.data;
				console.log(this.onedatapl)
			})

	  	},
	  	backa(){
	  		window.history.go(-1)
	  	},
	  	
	  },
	  created(){
	  	this.item_id=this.$route.query.item_id;
	  	console.log(this.item_id);
	  	this.shujua();
	  	this.shujub();
	  }
	}
</script>
<style scoped>
.banner{
	height: 200px;
}
.banner img{
	width: 100%;
	height: 100%;

}
.pl{

}
.pl .p1{
	width: 100%;
	line-height: 30px;

}
.pl .p1 span{
	display: inline-block;
	width: 60px;
	border-bottom: 2px solid #000;
	text-align: center;
}
.pl .hf{
	width: 80%;
	margin:0 auto;
	padding: 5%;
	border: 1px solid #999;
}
</style>