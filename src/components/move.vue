<template>
	<div>
		<div>
			<mt-header fixed  title="电影">
				<div slot="left" @click="backa()">
			    <mt-button icon="back"></mt-button>
			  </div>
			  
			</mt-header>
			
		</div>
		<div v-for="itm in onedata" class="move">
			<div @click="fn(itm.item_id)">
				<mt-cell  :title="itm.subtitle" :label="itm.title" >
				  <img slot="icon" :src="itm.img_url" width="24" height="24">
				</mt-cell>
			</div>
			
		</div>
		
	</div>
</template>
<script>
	import Vue from 'vue'
	import axios from 'axios'
	export default {
	  name: 'move',
	  data () {
	    return {
	      onedata:'',
	     
	    }
	  },
	  methods:{
	  	shujua(){
	  		axios({
			  method:'get',
			  url: 'http://v3.wufazhuce.com:8000/api/channel/movie/more/0?channel=wdj&version=4.0.2&uuid=ffffffff-a90e-706a-63f7-ccf973aae5ee&platform=android'
			})
			.then(response => {
				this.onedata=response.data.data;
				console.log(this.onedata)
			})

	  	},
	  	fn(item_id){
	  		this.$router.push({path:'/movexx',query:{item_id:item_id}});
	  	},
	  	backa(){
	  		window.history.go(-1)
	  	},
	  },
	  created(){
	  	this.shujua()
	  }
	}
</script>
<style scoped>
	.move{
		border: 
	}
</style>
