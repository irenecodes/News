<template>
    <!-- <div class="marquee3k" 
        data-speed="0.25" 
        data-reverse="bool" 
        data-pausable="bool">
        <p 
            v-for="(article, i) in this.$store.state.marqueeNews"
            :key="i">

        </p>
    </div> -->
    <div>

    </div>
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
    mounted(){
        // Marquee3k.init()
    }

}
</script>

<style>

</style>