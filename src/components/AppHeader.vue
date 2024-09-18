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
					// svuoto il campo dell'input dopo aver visualizzato i titoli
					this.searchText = ''
				},
				// funzione per gestire le bandiere
				flag(language){
					// salvo i dati delle lingue che hanno una corrispondenza con le immagini
					const validLanguage = [
						'en',
						'it',
						'ja',
						'de',
						'pt',
						'es',
						'fr',
						'dk'
					];
					// se sono valide...
					if(validLanguage.includes(language)){

						// quando foto e dicitura non corrispondono, associo la dicitura
						if(language == 'en'){
							return 'img/flags/gb.webp'
						}
						else if(language == 'ja'){
							return 'img/flags/jp.webp'
						}
						// altrimenti concateno
						else{
							return 'img/flags/' + language + '.webp'
						}
					}
					// altrimenti ¯\_(ツ)_/¯
					else{
							return 'img/flags/idk.gif'
						}
				}
			},
	}
</script>

<template>
	<header>

		<div class="container">

			<!-- input form per la ricerca dei film -->
			<div class="input-group mb-3">
				<!-- input con v-model per collegarlo al data searchText -->
				<input v-model="searchText" type="text" class="form-control" placeholder="Cosa vuoi vedere?">

				<!-- bottone da cui ascolto il click per cercare i film/serie tv -->
				<button @click="searchMovie()" class="btn btn-outline-secondary" type="submit">
					<i class="fa-solid fa-magnifying-glass"></i>
				</button>
			</div>

		</div>
	</header>

	<main>

		<div class="container">

			<div class="row">

				<!-- ciclo per ripetere la card con le info dei film -->
				<div class="col mb-3" v-for="(movie, i) in movies" :key='i'>

					<!-- card in cui compaio le infomrazioni del film -->
					<div class="card">
							<img src="..." class="card-img-top" alt="...">
						<div class="card-body">
							<h5 class="card-title">Titolo: {{movie.title}}</h5>
						</div>
						<ul class="list-group list-group-flush">
							<li class="list-group-item">Titolo originale: {{movie.original_title}}</li>
							<li class="list-group-item">Lingua originale: <img :src="flag(movie.original_language)" alt="" class="imgLanguage"></li>
							<li class="list-group-item">Voto: {{movie.vote_average}}</li>
						</ul>
					</div>

				</div>

			</div>

		</div>

	</main>

</template>

<style>
	.imgLanguage{
		width: 100px;
		border-radius: 5px;
	}
</style>