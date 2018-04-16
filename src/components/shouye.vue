<template>
	<div>
		<div class="div">
			<p>阅读</p>
			<p><router-link to="/move">影视</router-link></p>
			<div v-for="itm in onedata">
				<p v-for="itam in itm.tag_list">{{itam.title}}</p>
				<p @click="fn(itm.item_id)">{{itm.title}}</p>
				<p><img :src="itm.img_url" alt=""></p>
				<p>{{itm.forward}}</p>
			</div>
		</div>
		
	</div>
</template>
<script>
import Vue from 'vue'
import axios from 'axios'
export default {
  name: 'shouye',
  data () {
    return {
      onedata:'',
      content_list:''
    }
  },
  methods:{
  	shujua(){
  		axios({
		  method:'get',
		  url: 'http://v3.wufazhuce.com:8000/api/channel/reading/more/0?channel=wdj&version=4.0.2&uuid=ffffffff-a90e-706a-63f7-ccf973aae5ee&platform=android'
		})
		.then(response => {
			this.onedata=response.data.data;
			console.log(this.onedata)
		})

  	},
  	fn(item_id){
  		this.$router.push({path:'/xianxi',query:{item_id:item_id}});
  	}
  },
  created(){
  	this.shujua()
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
</style>