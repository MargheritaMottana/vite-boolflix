<script>

	// installato ed importato axios per fare la chiamata API
  	import axios from 'axios'

	export default {
			data() {
				return { 
					searchText: '',
					APIKey: '796dd0c05d6cbaf28484679c71b661a0',
					movies: [],
				}
			},
			methods:{
				// aggiungo il metodo a cui si appoggia il bottone per la ricerca API
				searchMovie(){
					// chiamata con due parametri
					axios.get('https://api.themoviedb.org/3/search/movie',{
						params:{
							api_key: this.APIKey,
							query: this.searchText,
						}
					})
					// risposta che scrive nell'array il dato dell'API che mi serve
					.then((resp) => {
						// console.log(resp.data.results)
						this.movies = resp.data.results;
					})
				}
			},
	}
</script>

<template>
	<header>
		<!-- input form per la ricerca dei film -->
		<div class="input-group mb-3">
			<!-- input con v-model per collegarlo al data searchText -->
  			<input v-model="searchText" type="text" class="form-control" placeholder="Cosa vuoi vedere?">

			<!-- bottone da cui ascolto il click per cercare i film/serie tv -->
  			<button @click="searchMovie()" class="btn btn-outline-secondary" type="submit">
				<i class="fa-solid fa-magnifying-glass"></i>
			</button>
		</div>
	</header>

	<main>
		<div>
			<div class="card" style="width: 18rem;">
					<img src="..." class="card-img-top" alt="...">
				<div class="card-body">
					<h5 class="card-title">Titolo</h5>
				</div>
				<ul class="list-group list-group-flush">
					<li class="list-group-item">Titolo Originale</li>
					<li class="list-group-item">Lingua</li>
					<li class="list-group-item">Voto</li>
				</ul>
			</div>
		</div>
	</main>
	
</template>