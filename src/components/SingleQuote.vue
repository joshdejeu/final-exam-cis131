<template>
  <div id="single_quote">
    <h1>{{author}}</h1>
    <h2>"{{newQuote}}"</h2>
    <!-- when clicked it will call the API again -->
    <input id="btn" type="button" value="Next" @click="callAPIagain">
  </div>
</template>

<script>
// this allows axios to work when we call the API again
import axios from 'axios'

export default {
  name: 'SingleQuote',
  components: {
    
  },
  props:{
      author: String,
      text: String,
  },
  data(){
    return{
        newLink: `https://quote-garden.herokuapp.com/api/v3/quotes?author=${this.author}`,
        // because props can not be changes we will initially set the innerHTML to be the prop
        // but we can also change it now because it is a 'data' variable 
        newQuote: this.text,
    }
  },
  methods:{
    // now that we have the author, we want their quotes so we call a new API
    callAPIagain(){
        axios
        .get(this.newLink)
        .then(response =>{
            // the index will be a ranom number from 0 to the length of the array the API sends back
            var i = this.generateRandomNumber(response.data.data.length);

            //now we update the quote data variable, we would not be able to do this if it was a prop
            this.newQuote = response.data.data[i].quoteText;
        })
    },
    generateRandomNumber(arrayLength){
        // a random number from 0 to 10 will be created and returned
        var number = Math.floor(Math.random()*arrayLength);
        return number;
    }
  }
}
</script>

<style scoped>
#single_quote{
    border: 1px solid rgb(150,150,150);
    border-radius: 20px;
    width: 60%;
    height: 150px;
    margin: 20px 0px;
    padding: 10px;
    display: grid; grid-template-rows: 1fr 5fr 1fr;
}
h1,h2{
    font-family: 'Segoe UI', sans-serif;
}
h1{
    font-size: 25px;
}
h2{
    font-size: 15px;
    font-weight: 100;
}
#btn{
    width: 50px; height: 25px;
    border-radius: 5px; outline: none; border: none;
    cursor: pointer;
    transition: 0.3s ease;
}
#btn:hover{
    background: rgb(192, 203, 255);
}

#btn2{
    width: 70px; height: 25px; margin-right: 20px;
    border-radius: 5px; outline: none; border: none;
    cursor: pointer;
    transition: 0.3s ease;
}
#btn2:hover{
    background: rgb(192, 203, 255);
}
</style>
