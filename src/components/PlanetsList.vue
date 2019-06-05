<template>
	<div class="col-md-8">
  		<div class="panel panel-success">
  			<div class="panel-heading">
  				<div class="panel-title">
  					<h4>Planets:</h4>   
  				</div>
  			</div>
  			<div class="panel-body">
  				<div v-for="(planets, index) in planetsInfo" :key="`planets_${index}`" class="col-md-4"  >
                   {{ planets.name }}			
          	    </div>
  			</div>
  		</div>
  	</div>
</template>

<script>
  export default {
    name: 'planetsList',
    props: [
      'planetsInfo',
		],
}
  
</script>