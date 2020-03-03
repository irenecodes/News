<template>
  <div class="container">
    <marquee-scroll></marquee-scroll>

    <header>
      <div class="pimg1">
        <div class="ptext">
          <h1>Breaking News</h1>
        </div>
      </div>
    </header>

    

    <section class="section section-light">
      <h2>Section One</h2>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Odio, at expedita neque minima pariatur enim animi repudiandae quo, reprehenderit quaerat rerum minus impedit corporis labore. Aspernatur, fugiat veniam iure aliquam minima quisquam non, pariatur quos laudantium expedita quaerat eos doloremque corporis suscipit laborum quidem accusamus ut neque, sequi beatae maiores mollitia? Nobis, a et quam doloremque exercitationem laboriosam perferendis veritatis blanditiis nostrum sequi iste illo fugiat, quae voluptate qui voluptatum, sit provident. Quam amet adipisci recusandae excepturi nobis? Porro unde enim temporibus alias laudantium nemo distinctio, blanditiis saepe dolorum quisquam rerum quia quam maiores reprehenderit voluptate assumenda suscipit esse? Unde.</p>
    </section>

    <div class="pimg2">
      <div class="ptext">
        <span class="border">Image Two Text</span>
      </div>
    </div>

    <section class="section section-dark">
      <h2>Section Two</h2>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Odio, at expedita neque minima pariatur enim animi repudiandae quo, reprehenderit quaerat rerum minus impedit corporis labore. Aspernatur, fugiat veniam iure aliquam minima quisquam non, pariatur quos laudantium expedita quaerat eos doloremque corporis suscipit laborum quidem accusamus ut neque, sequi beatae maiores mollitia? Nobis, a et quam doloremque exercitationem.</p>
    </section>

    <div class="pimg3">
      <div class="ptext">
        <span class="border">Image 3 Text</span>
      </div>
    </div>

    <section class="section section-dark">
      <h2>Section Three</h2>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Odio, at expedita neque minima pariatur enim animi repudiandae quo, reprehenderit quaerat rerum minus impedit corporis labore. Aspernatur, fugiat veniam iure aliquam alias laudantium nemo distinctio, blanditiis saepe dolorum quisquam rerum quia quam maiores reprehenderit voluptate assumenda suscipit esse? Unde.</p>
    </section>

    




  
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
      latestArticle: [],
      

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
        this.latestArticle = results.articles[0]

        console.log(this.breakingNews)
      })
  },

  methods: {

  }
}
</script>