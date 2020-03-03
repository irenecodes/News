<template>
    <div class="ticker-wrap">
        <div 
            class="ticker"
            v-for="(article, i) in marqueeNews"
            :key="i"
        >
            <a :href="article.url" target=_blank>
                {{article.title}}
            </a>
        </div>
    </div>
</template>


<script>

export default {
    data(){
        return {
            apiKey: process.env.API_KEY,
            marqueeNews: null,
        }
    },
    async created(){
        var categoryUrl = 'http://newsapi.org/v2/top-headlines?' + 'country=ca&' + 'category=health&' + 'apiKey=' + this.apiKey;
        fetch(categoryUrl)
            .then(results => results.json())
            .then(results => {
                this.marqueeNews = results.articles.splice(0,5)
                console.log(this.marqueeNews)

                
            })
    },
    mounted(){

    }

}
</script>

<style>

</style>