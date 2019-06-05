<template>
	<div class="col-md-8">
  		<div class="panel panel-success">
  			<div class="panel-heading">
  				<div class="panel-title">
  					<h4>StarShips:</h4> 
  				</div>
  			</div>
  			<div class="panel-body">  	
                <div v-for="(ship, index) in shipsInfo" :key="`ship_${index}`"  class="col-md-4" >
                   {{ ship.name }}		  
          	    </div>			     
                  
          	</div>  			
  		</div>
  	</div>
</template>

<script>
  export default {
    name: 'starshipsList',
    props: [
      'shipsInfo',
		],
}
  
</script>