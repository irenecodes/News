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



    <footer></footer>
    
  </div>

</template>

<script>
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
      breakingNews: null,




    }
  },
  computed: {

  },
  async created(){
    var url = 'http://newsapi.org/v2/top-headlines?' + 'country=us&' + 'apiKey=' + this.apiKey;
      
    fetch(url)
      .then(results => results.json())
      // returns info as a json object
      .then(results => {
        console.log(results)

        this.breakingNews = results.articles.splice(0,3)
        console.log(this.breakingNews)
      })

    
    
  },

  methods: {
    




  }
}
</script>