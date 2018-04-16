<template>
	<div>
		<div>
			<mt-header fixed  :title="onedata.hp_title">
				<div slot="left" @click="backa()">
			    <mt-button icon="back"></mt-button>
			  </div>
			  
			</mt-header>
			
		</div>
		
		<div class="wz">
			<p>{{onedata.hp_title}}</p>
			<p>文/{{onedata.hp_author}}</p>
			<div v-html="onedata.hp_content"></div>
		</div>
		<div class="wz_zz">
			<p class="p1"><span>作者</span></p>
			<div v-for="itm in onedata.author">
				<p><img width="60" :src="itm.web_url" alt=""></p>
				<p><span><b>{{itm.user_name}}</b></span><span>{{itm.summary}}</span></p>
			</div>
		</div>
		<div class="wz_zz">
			<p class="p1"><span>评论列表</span></p>
			<div v-for="itm in onedatapl.data">
				<p><span><img width="30" :src="itm.user.web_url" alt="">{{itm.user.user_name}}</span><span>{{itm.input_date}}</span></p>
				<p><span><b></b></span><span>{{itm.content}}</span></p>
			</div>
		</div>
		


	</div>
</template>
<script>
import Vue from 'vue'
import axios from 'axios'
export default {
  name: 'xianxi',
  data () {
    return {
      item_id:'',
      onedata:'',
      onedatapl:'',
     
    }
  },
  methods:{
  	shujua(){
  		axios({
		  method:'get',
		  url: 'http://v3.wufazhuce.com:8000/api/essay/' + this.item_id + '?channel=wdj&source=channel_reading&source_id=9264&version=4.0.2&uuid=ffffffff-a90e-706a-63f7-ccf973aae5ee&platform=android'
		})
		.then(response => {
			this.onedata=response.data.data;
		 //console.log(response.data);
		})

  	},
  shujub(){
  	axios({
		  method:'get',
		  url: 'http://v3.wufazhuce.com:8000/api/comment/praiseandtime/essay/ '+ this.item_id + '/0?channel=wdj&version=4.0.2&uuid=ffffffff-a90e-706a-63f7-ccf973aae5ee&platform=android'
		})
		.then(response => {
			this.onedatapl=response.data.data;
		 //console.log(this.onedatapl);
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
  	this. shujub();
  }
  	
}
</script>
<style scoped>
.div{
	max-width: 750px;
	margin:0 auto;
}
.div img{
	width: 100%;
}
.wz_zz .p1{
	width: 100%;
	height: 20px;
	line-height: 20px;
}
.wz_zz .p1 span{
	display: inline-block;
	width: 80px;
	border-bottom: 2px solid #000;
}
.one-img-container{
	width: 100%;
}
</style>