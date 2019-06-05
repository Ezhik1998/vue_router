<template>
    <div>
        <h2>{{character.name}}</h2>        
        Height: {{character.height}}<br/>
        Mass: {{character.mass}}<br/>
        Birth: {{character.birth_year}}<br/>
        Hair color: {{character.hair_color}}<br/>
        Skin color: {{character.skin_color}}<br/>
        Eye color: {{character.eye_color}}<br/>
        Homeworld: {{homeInfo.name}}<br/>

        <div class = "row" >            
            <h4>Species:</h4>      
            <div v-for="(species, index) in speciesInfo" :key="`species_${index}`"  class="col-md-4" >
                   {{ species.name }}			
          	</div>    
        </div> 
         
        <div class = "row" >  
          <films-list :filmsInfo="filmsInfo"></films-list>            
        </div> 
        <div v-if ='character.vehicles && character.vehicles.length > 0'>            
            <div class = "row" >
              <vehicles-list :vehiclesInfo="vehiclesInfo"></vehicles-list>         
            </div>
        </div>
        <div v-if ='character.starships && character.starships.length > 0'>            
            <div class = "row" >     
                <ships-list :shipsInfo="shipsInfo"></ships-list>  
          	</div>    
        </div>    
        <router-link to="/">Back</router-link>
    </div>
</template>


<script>
import axios from 'axios';
import FilmsList from '@/components/FilmAppeared';
import VehiclesList from '@/components/VehiclesList';
import ShipsList from '@/components/StarshipsList'
export default {
  data: () => ({      
      character: [],  
      filmsInfo: [],
      vehiclesInfo: [],
      shipsInfo: [],
      homeInfo: [],
      speciesInfo: [],
      
  }), 
  components: {
    FilmsList,
    VehiclesList,
    ShipsList,     
  },
  
  async created() {
    const {data} = await axios.get('https://swapi.co/api/people/'+this.$route.params.id);
    this.character = data 

    this.character.films.forEach((filmUrl) => {
          fetch(filmUrl).then((response) => {
            return response.json();
          }).then((detail) => {
            let parse_url = detail.url.split('/');
            detail.id = parse_url[parse_url.length - 2]; 
            this.filmsInfo.push(detail);                       
          })
        }); 


    this.character.species.forEach((speciesUrl) => {
          fetch(speciesUrl).then((response) => {
            return response.json();
          }).then((detail) => {
            let parse_url = detail.url.split('/');
            detail.id = parse_url[parse_url.length - 2]; 
            this.speciesInfo.push(detail);                       
          })
        }); 
        

    this.character.vehicles.forEach((vehicleUrl) => {
          fetch(vehicleUrl).then((response) => {
            return response.json();
          }).then((detail) => {
            let parse_url = detail.url.split('/');
            detail.id = parse_url[parse_url.length - 2]; 
            this.vehiclesInfo.push(detail);                       
          })
        }); 

    this.character.starships.forEach((shipUrl) => {
          fetch(shipUrl).then((response) => {
            return response.json();
          }).then((detail) => {
            let parse_url = detail.url.split('/');
            detail.id = parse_url[parse_url.length - 2]; 
            this.shipsInfo.push(detail);                       
          })
        }); 
    
    fetch(this.character.homeworld).then((response) => {
            return response.json();
          }).then((detail) => {
            let parse_url = detail.url.split('/');
            detail.id = parse_url[parse_url.length - 2];
            this.homeInfo = detail;                                 
          })
    }
        // console.log(this.vehiclesInfo);
}   

</script>