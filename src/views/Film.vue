<template>
    <div>
        <h2>{{film.title}}</h2>
        <p v-if="film.director">
        Director: {{film.director}}<br/>
        Released: {{film.release_date}}<br/>
        </p>     
        <div class = "row">
          {{film.opening_crawl}}
        </div>   
        <div class="row">
	  	      <character-list :details="characterDetails"></character-list>
	      </div>
                  
        <div class = "row" >     
            <ships-list :shipsInfo="shipsInfo"></ships-list>  
        </div>    
        
        
        <div class = "row">
          <planets-list :planetsInfo="planetsInfo"></planets-list>          
        </div>

        <div class = "row" >
              <vehicles-list :vehiclesInfo="vehiclesInfo"></vehicles-list>         
            </div>

        <div class="row">
	  	      <species-list :speciesInfo="speciesDetails"></species-list>
	      </div>
        <p/>
        <router-link to="/">Back</router-link>
    </div>
</template>

<script>
import axios from 'axios';
import CharacterList from '@/components/CharacterList';
import SpeciesList from '@/components/SpeciesList';
import ShipsList from '@/components/StarshipsList';
import VehiclesList from '@/components/VehiclesList';
import PlanetsList from '@/components/PlanetsList';
export default {
  data: () => ({
      film: {},      
      characterDetails: [], 
      speciesDetails: [], 
      planetsInfo: [],
      shipsInfo: [],
      vehiclesInfo: [],

  }), 
  components: {    
    CharacterList, 
    SpeciesList, 
    ShipsList,
    VehiclesList,
    PlanetsList
  },
  
  async created() {
    var {data} = await axios.get('https://swapi.co/api/films/'+this.$route.params.id);
    this.film = data      

    this.film.characters.forEach((characterUrl) => {
          fetch(characterUrl).then((response) => {
            return response.json();
          }).then((detail) => {
            let parse_url = detail.url.split('/');
            detail.id = parse_url[parse_url.length - 2]; 
            this.characterDetails.push(detail);                       
          })
        }); 
    
    this.film.planets.forEach((planetUrl) => {
          fetch(planetUrl).then((response) => {
            return response.json();
          }).then((detail) => {
            let parse_url = detail.url.split('/');
            detail.id = parse_url[parse_url.length - 2]; 
            this.planetsInfo.push(detail);                       
          })
        }); 

    this.film.vehicles.forEach((vehicleUrl) => {
          fetch(vehicleUrl).then((response) => {
            return response.json();
          }).then((detail) => {
            let parse_url = detail.url.split('/');
            detail.id = parse_url[parse_url.length - 2]; 
            this.vehiclesInfo.push(detail);                       
          })
        });

    this.film.starships.forEach((shipUrl) => {
              fetch(shipUrl).then((response) => {
                return response.json();
              }).then((detail) => {
                let parse_url = detail.url.split('/');
                detail.id = parse_url[parse_url.length - 2]; 
                this.shipsInfo.push(detail);                       
              })
            });
    this.film.species.forEach((speciesUrl) => {
          fetch(speciesUrl).then((response) => {
            return response.json();
          }).then((detail) => {
            let parse_url = detail.url.split('/');
            detail.id = parse_url[parse_url.length - 2]; 
            this.speciesDetails.push(detail);                       
          })
        }); 

  }  
}
</script>