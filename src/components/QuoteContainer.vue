<template>
  <div id="QuoteContainer">
    <div id="QuoteContainer_container" v-for="obj in objs" :key="obj.key">
        <SingleQuote :author="obj.quoteAuthor" :text="obj.quoteText"/>
    </div>

  </div>
</template>

<script>
// this allows axios to work when we call the API
import axios from 'axios'
import SingleQuote from './SingleQuote.vue'

export default {
  name: 'QuoteContainer',
  components: {
    SingleQuote
  },
  data(){
      return{
        link: 'https://quote-garden.herokuapp.com/api/v3/quotes',
        author: '',
        quote: '',
        objs: [],
      }
  },
  mounted(){
      // on page load we will call the API
      this.callAPI();
  },
  methods:{
      callAPI(){
        axios
        .get(this.link)
        .then(response =>{
            //the objs data variable will now hold objects from the API
            this.objs=response.data.data;   
        })
      },

  }
}
</script>

<style scoped>
#QuoteContainer_container{
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
</style>
