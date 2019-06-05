<template>
	<div class="col-md-8">
  		<div class="panel panel-success">
  			<div class="panel-heading">
  				<div class="panel-title">
  					<h4>Vehicles:</h4> 
  				</div>
  			</div>
  			<div class="panel-body">           
                <div v-for="(vehicle, index) in vehiclesInfo" :key="`vehicle_${index}`"   class="col-md-4" >
                   {{ vehicle.name }}			
          		</div>   			
  		    </div>
  	    </div>
	</div>
</template>

<script>
  export default {
    name: 'vehiclesList',
    props: [
      'vehiclesInfo',
		],
}
  
</script>