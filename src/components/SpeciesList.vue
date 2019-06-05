<template>
	<div class="col-md-8">
  		<div class="panel panel-success">
  			<div class="panel-heading">
  				<div class="panel-title">
  					<h4>Species</h4>
  				</div>
  			</div>
  			<div class="panel-body">
  				<div v-for="(species, index) in speciesInfo" :key="`species_${index}`"  class="col-md-4" >
                    <router-link :to="{ name:'species', params:{id:species.id} }">{{ species.name }}</router-link>				
                   			
          	</div>
  			</div>
  		</div>
  	</div>
</template>

<script>
  export default {
    name: 'speciesList',
    props: [
      'speciesInfo',
		],
}
  
</script>