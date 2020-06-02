<template>
  <div>
    <b-card  
    style="max-width: 13rem;" 
    class="mb-3" 
    :title="result.title" 
    v-bind:img-src="'http://image.tmdb.org/t/p/w500/' + result.poster_path" 
    v-bind:img-alt="'Poster image of ' + result.title + ' from tMDB'" 
    img-top>
        <b-card-text>
            <p>{{ result.overview}}</p>
            <p>Vote Average:</p>
            <p>{{ result.vote_average}}</p>
            
        </b-card-text>
        <template v-slot:footer>
            <small class="text-muted">Release Date: {{ result.release_date }}</small>
        </template>
    </b-card>
  </div>
</template>

<script>
export default {
	props: {
		result: Object
    },
    methods: {
    }
}
</script>