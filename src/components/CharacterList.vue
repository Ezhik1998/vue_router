<template>
	<div class="col-md-8">
  		<div class="panel panel-success">
  			<div class="panel-heading">
  				<div class="panel-title">
  					<h4>Characters</h4>
  				</div>
  			</div>
  			<div class="panel-body">
  				<div v-for="(characterDetail, index) in details" class="col-md-4" :key="index">
          	<router-link :to="{ name:'character', params:{id:characterDetail.id} }">{{ characterDetail.name }}	</router-link>				
          <!-- <router-link :to="{ name:'character' }">{{ details[index].name }}	</router-link>				 -->
        
				</div>
  			</div>
  		</div>
  	</div>
</template>

<script>
  export default {
    name: 'characterList',
    props: [
      'details',
		],
}
  
</script>