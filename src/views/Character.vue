<template>
    <div>
        <h2>This page is an character page with id {{$route.params.id}}</h2>
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
            <div v-for="(specy, index) in speciesInfo" :key="`specy_${index}`"  class="col-md-4" >
                   {{ specy.name }}			
          	</div>    
        </div> 
         
        <div class = "row" >   
            <h4>Films:</h4>      
            <div v-for="(film, index) in filmsInfo" :key="`film_${index}`"  class="col-md-4" >
                   {{ film.title }}			
          	</div>    
        </div> 
        <div v-if ='character.vehicles && character.vehicles.length > 0'>            
            <div class = "row" >    
                <h4>Vehicles:</h4>     
                <!-- <vehicles-list :vehiclesCharacter="vehiclesInfo"></vehicles-list>         -->
                <div v-for="(vehicle, index) in vehiclesInfo" :key="`vehicle_${index}`"   class="col-md-4" >
                   {{ vehicle.name }}			
          		</div>
            </div>
        </div>
        <div v-if ='character.starships && character.starships.length > 0'>
            
            <div class = "row" >     
                <h4>StarShips:</h4>    
                <div v-for="(ship, index) in shipsInfo" :key="`film_${index}`"  class="col-md-4" >
                   {{ ship.name }}			
          		</div>    
            </div>
        </div>


        <!-- <div class="row">
	  	      <character-details :details="characterDetails"></character-details>
	      </div> -->

        <router-link to="/">Back</router-link>
    </div>
</template>


<script>
import axios from 'axios';

export default {
  data: () => ({      
      character: [],  
      filmsInfo: [],
      vehiclesInfo: [],
      shipsInfo: [],
      homeInfo: [],
      speciesInfo: [],
  }), 
  
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

    this.character.species.forEach((specyUrl) => {
          fetch(specyUrl).then((response) => {
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