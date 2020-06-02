<template>
 
  <div class="m-4">

    <b-tabs content-class="m-3">
      <!-- <div class="mx-auto"> -->
        <!-- first tab -->
      <b-tab title="Trending Now" active>
      <b-row>
        <!-- radio form -->
        <b-col class="col-md-3">
          <b-container class="mt-5">
            <b-card bg-variant="light">
            <b-form-group label="Trending Period">
                  <b-form-radio v-model="selected" name="trend-period" value="week" @change="getTestResults">Week</b-form-radio>
                  <b-form-radio v-model="selected" name="trend-period" value="day" @change="getTestResults">Day</b-form-radio>
              </b-form-group>
            </b-card>  
          </b-container>
          
        </b-col>
        <!-- trending content -->
        <b-col class="col-md-9">
          <intro v-if="selected === null">
            <p slot="title" class="text-center">Select a Trending Period to see results</p>
          </intro>

          <intro v-else>
            <p slot="title" class="lead">Trending {{trendPeriodText}}</p>
            <p slot="content">
              Here are the top 20 movies trending {{trendPeriodText}} according to 
              <a href="https://developers.themoviedb.org/3/trending/get-trending"
              target="_blank">tMDB</a>. 
              {{ trendPeriodDefinition }}
              </p>
          </intro>
          <b-card-group deck>
            <CardDeck 
            v-for="result in testResults" 
            :key="result.id" 
            :result="result" />
            </b-card-group> 
          
          </b-col>
        </b-row>
      </b-tab>
        <!-- second tab -->
      <b-tab title="Other Trend">
        <p>I'm the other tab</p>
        </b-tab>
        <!-- </div> -->
    </b-tabs>

  </div>

</template>

<script>
import Intro from '~/components/intro.vue';
import CardDeck from '~/components/CardDeck.vue';
import axios from 'axios';

export default {
    components: {
      Intro,
      CardDeck
    },
    data() {
        return {
          selected: null,
          loading: true,
          testResults: null,
          errored: false
        }
    },
    computed: {
      trendPeriodText() {
        let leadingText;
        if (this.selected === 'day') {
          return leadingText = 'today';
        } else {
          return `this ${this.selected}`;
        }; 
      },
      trendPeriodDefinition() {
        let definition;
        if (this.selected === 'day') {
          definition = 'The daily trending list tracks items over the period of a day while items have a 24 hour half life.';
        } else {
          definition = 'The weekly list tracks items over a 7 day period, with a 7 day half life.';
        };
        return definition; 
      }

    },
    methods: {
         getTestResults(event) {
          let apicall = 'https://api.themoviedb.org/3/trending/movie/' + event + '?api_key=890f4b3dccb1250594537c39d4d51fd9';
           axios.get(apicall).then(response => { this.testResults = response.data.results });
        }
    },
    mounted () {
        // axios.get('https://api.themoviedb.org/3/trending/movie/week?api_key=890f4b3dccb1250594537c39d4d51fd9')
        // .then(response => (this.weeklyResults = response.data.results))
        // .catch(error => {console.log(error)
        // this.errored = true})
        // .finally(() => this.loading = false)
    }  
}
</script>

<style>

</style>