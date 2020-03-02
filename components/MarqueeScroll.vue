<template>
  <p>Marquee Scroll</p>
</template>

<script>
export default {
    data(){
        return {
            apiKey: process.env.API_KEY
        }
    },
    async created(){
        var categoryUrl = 'http://newsapi.org/v2/top-headlines?' + 'country=ca&' + 'category=health&' + 'apiKey=' + this.apiKey;


        fetch(categoryUrl)
            .then(results => results.json())
            .then(results => {
                this.$store.state.marqueeNews = results.articles.splice(0,5)
                console.log(this.$store.state.marqueeNews)
            })
    },

}
</script>

<style>

</style>