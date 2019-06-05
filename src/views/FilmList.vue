<template>
<div>
  <div class="row" v-for="film in films" :key="film.episode_id">	
		<router-link :to="{ name:'film', params:{id:film.id} }">{{ film.title }}</router-link>
  </div>
</div>
</template>

<script>
import axios from 'axios';
export default {
  data: () => ({
    films:[]
  }), 
  
  async created() {
    const {data} = await axios.get("https://swapi.co/api/films/");
    this.films = data.results.map(film => {
      let parse_url = film.url.split('/');
      film.id = parse_url[parse_url.length - 2];
      
      return film;
    });
  }
  
}
</script>

