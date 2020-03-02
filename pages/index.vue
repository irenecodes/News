<template>
  <div class="container">
    <header>
      <marquee-scroll></marquee-scroll>
      <h1>Breaking News</h1>
    </header>
  
    <section>
      <div class="card-container">
        <div 
          v-for="(news, i) in breakingNews"
          :key="i"
          class="card"
        >
          <h3>{{news.title}}</h3>

          <div>
            <a :href="news.url" target="_blank">
              <img :src="news.urlToImage" alt="">
            </a>
          </div>
          <p>{{news.description}}</p>
          <h4>By: {{news.author}}</h4>
          <p>Published on: {{news.publishedAt | moment("dddd, MMMM Do YYYY") }}</p>
          
        </div>
      </div>
    </section>

    <section>
      <h2>What would you like to know about?</h2>
      Topic
      <!-- <input type="text"> -->

      In between which days would you like to know about?
      <!-- datepicker here -->
    </section>

    Famous Deaths from this day In history

    Famous births from this day in history

    <section>
      Looking for a future event? See what's coming up on: 
      <!-- input for date -->
      at
      <!-- input for location  -->
    </section>



    <footer></footer>
    
  </div>

</template>

<script>
// import moment from 'moment'
// import tz from 'moment-timezone'

import Logo from '~/components/Logo.vue'
import MarqueeScroll from '~/components/MarqueeScroll.vue'
import ShareOnTwitter from '~/components/ShareOnTwitter.vue'
import Footer from '~/components/Logo.vue'



export default {
  components: {
    Logo,
    MarqueeScroll,
    ShareOnTwitter,
    Footer
  },
  mounted(){

  },
  data(){
    return {
      apiKey: process.env.API_KEY,
      breakingNews : [],
      

    }
  },
  computed: {

  },
  async created(){
    var vm = this
    var url = 'http://newsapi.org/v2/top-headlines?' + 'country=ca&' + 'apiKey=' + this.apiKey;
      
    fetch(url)
      .then(results => results.json())
      // returns info as a json object
      .then(results => {
        this.breakingNews = results.articles.splice(0,3)
        console.log(this.breakingNews)

      })
  },

  methods: {

  }
}
</script>