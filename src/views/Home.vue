<template>
<div>
	<ul>
		<li v-for="film in films" :key="film.episode_id">
      {{film.title}}
		<!-- <router-link :to="{ name:'film', params:{id:film.id} }">{{ film.title }}</router-link> -->
		</li>
	</ul>
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
    console.log(data);
    this.films = data.results;
    // console.log(this.films);
    return this.films;
  }
  
}
</script>

