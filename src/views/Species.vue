<template>
    <div>
        <h2>{{species.name}}</h2>
        Classification: {{species.classification}}<br/>
        Designation: {{species.designation}}<br/>
        Average height: {{species.average_height}}<br/>
        Skin colors: {{species.skin_colors}}<br/>
        Hair colors: {{species.hair_colors}}<br/>
        Eye colors: {{species.eye_colors}}<br/>
        Average lifespan: {{species.average_lifespan}}<br/>
        Language: {{species.language}}<br/>

    </div>
    
</template>

<script>
import axios from 'axios';
export default {
    data: () => ({
      species: [],       
    }),

    async created() {
    var {data} = await axios.get('https://swapi.co/api/species/'+this.$route.params.id);
    this.species = data 
    }
    
}
</script>
