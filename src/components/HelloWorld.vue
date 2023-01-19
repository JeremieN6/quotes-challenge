<template>
   <!--<div class="hello">
    <div v-for="item in quotes" v-bind:key="item._id" >
      <p style="color: blue;">{{item.content}}</p>
      <span style="color: red;">{{ item.author }}</span>
      </div>
  </div> -->
  <div class="myheader">
        <div class="random" v-on:click="newQuote">
            {{refresh_quote}}
            <i class="fa fa-refresh" aria-hidden="true"></i>
        </div>
    </div>
    <div class="container_page">   <!--v-for="item in quotes" v-bind:key="item.content" -->              
        <div class="author" id="containerAuthor" v-show="true">
            {{currentQuote.author}}
        </div>
        <div class="container_quotes">
            <div class="quote">
                "{{currentQuote.content}}"
            </div>
            <div class="container_author_genre" id="container_author_genre" v-on:click="test">
                <div class="author_genre"> <!--v-for="item in quotes" v-bind:key="item.content" --> 
                    <div class="theAuthor">{{currentQuote.author}}</div>
                    <div class="genre" v-html="currentQuote.tags"></div>
                </div>
                <i class="fa fa-long-arrow-right" aria-hidden="true"></i>
            </div>
        </div>    
    </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',
  data(){
    return{
        quotes: null,
        currentQuote: {},
        authorQuote: {},
        tag: null,
        refresh_quote:"random",
    }
  },
  async created() {
    const response = await fetch('https://api.quotable.io/random');
    const data = await response.json();
    this.currentQuote = data;
  },
    methods:{
      test: function(){
          var container_author_genre = document.getElementById("container_author_genre");
          var containerAuthor = document.getElementById("containerAuthor");

          container_author_genre.style.display = "none";
          containerAuthor.style.display = "flex";
      },
      newQuote: function(){
        window.location.reload();
      }
  },
  mounted(){
    axios
    .get("https://api.quotable.io/random")
    .then((reponse) => {
      this.quotes = reponse;
      this.tags = reponse.data.tags;
      console.log(this.quotes);
    })
  }
}
</script>

<style>
@import url('https://fonts.cdnfonts.com/css/raleway-5');
@import url('https://fonts.cdnfonts.com/css/montserrat');

:root{
    /*COLOR*/
    --main-color: #333333;
    --second-color: #828282;
    --white-color: #FFFFFF;
    --third-color: #F7DF94;
    /*FONTS*/
    --main-font: 'Raleway';
    --footer-font: 'Montserrat';
}
.myheader{
    display: flex;
    justify-content: flex-end;
    margin: 1em 1em 0 0;
    position: absolute;
    top: 0;
    right: 0;
}
.container_page{
    position: absolute;
    top: 30%;
    width: 100%;
}
.author{
    display: none;
    justify-content: flex-start;
    align-items: flex-start;
    margin: 0em 2em 2em;
    padding-left: 1.5em;
    font-family: var(--main-font);
    font-style: normal;
    font-weight: 700;
    font-size: 16px;
    line-height: 42px;
    color: var(--main-color);
}
.random{
    font-family: var(--main-font);
    font-style: normal;
    font-weight: 500;
    font-size: 18px;
    line-height: 120%;
    color: var(--main-color);
    cursor: pointer;
}
.fa-refresh{
    color: var(--main-color);
    transform: rotate(90deg);
}
.container_quotes{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin: 0 0 5em 0;
    font-family: var(--main-font);
}
.quote{
    margin: 0em 2em 2em;
    border-left: 5px solid var(--third-color);
    padding-left: 1em;
}
.container_author_genre{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    width: 80%;
    background: var(--main-color);
    color: var(--white-color);
    height: 7em;
    cursor: pointer;
}
.genre{
    color: var(--second-color);
    font-size: 12px;
}
.fa-long-arrow-right{
    margin-right: 1em;
}
.author_genre{
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    padding-left: 1em;
}
footer{
    color: var(--second-color);
    font-family: var(--footer-font);
    font-size: 10px;
    display: flex;
    justify-content: center;
    position: absolute;
    bottom: 0;
    left: 20%;
}
@media (min-width:768px){
    .quote {
        width: 50%;
    }
    .container_author_genre {
        width: 50%;
    }
    .author {
        justify-content: center;
    }
    footer{
        color: var(--second-color);
        font-family: var(--footer-font);
        font-size: 10px;
        display: flex;
        justify-content: center;
        position: absolute;
        bottom: 0;
        right: 30%;
    }
}
</style>
