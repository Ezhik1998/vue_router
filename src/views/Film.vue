<template>
    <div>
        <h2>This page is an film page with id {{$route.params.id}}</h2>
        <h2>{{film.title}}</h2>
        <p v-if="film.director">
        Director: {{film.director}}<br/>
        Released: {{film.release_date}}<br/>
        </p>        
        <div class="row">
	  	      <character-list :details="characterDetails"></character-list>
	      </div>
        <router-link to="/">Back</router-link>
    </div>
</template>

<script>
import axios from 'axios';
import CharacterList from '@/components/CharacterList';
export default {
  data: () => ({
      film: {},
      characters: [],
      characterDetails: [],    
      date: '',
  }), 
  components: {    
    CharacterList,  
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
    
    
  //   methods: {
  //   filmDetails() {
  //     const filmID = this.$route.params.id;
  //     fetch(`http://swapi.co/api/films/${filmID}`).then((response) => {
  //       return response.json();
  //     }).then((j) => {
  //       this.results = j;
  //       this.date = j.release_date.slice(0, -6);

        
  //     });
  //   },
  // },



  }  
}
</script>