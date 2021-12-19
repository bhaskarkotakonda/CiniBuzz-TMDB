<template>
  <div id="app">
    <TopHeader @gotoCategory="reset"/>
    <div style="margin:140px 178px 0px 178px">
      <Search :moviequery="moviequery" @getResult="getResult"/>
      <CategoryBar v-if="CategoryPage" :categories="categories"/>
      <div v-if="SearchPage">
        <p style="position: absolute; width: 577px; height: 48px; left: 338px; top: 552px;font-family: Inter;font-style: normal;font-weight: normal;font-size: 40px;line-height: 48px; color: #000000;">Showing results for <strong>'{{moviequery}}'</strong></p>
          <div style="top:720px; position:absolute; margin-left: 178px; margin-right: 178px; width: 1288px; height: 1300px; flex-basis:25%; display:flex; flex-direction: row; flex-wrap: wrap; align-content: space-between;align-items: baseline; justify-content: space-between">
          <div v-for='result in results' :key='result.id'>
            <div style="margin-right:5px;" v-if="result.poster_path">
              <img class="posterimage"  v-bind:src="'http://image.tmdb.org/t/p/w500/' +    result.poster_path" >
              <p  align="left" style="max-width:250px; font-family: Inter;font-style: normal;font-weight: 600;font-size: 20px;line-height: 24px;">{{result.name}}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Search from './components/Search'
import TopHeader from './components/TopHeader'
import CategoryBar from './components/CategoryBar'
import Cards from './components/Cards'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Search, TopHeader, CategoryBar, Cards
  },
  data () {
    return {
      CategoryPage : true,
      SearchPage: false,
      DetailsPage : false,
      moviequery: '',
      categoryquery: '',
      moviename: '',
      results: [],
      categories: ['Upcoming', 'Popular', 'Drama', 'Thriller']
    }
  },
  methods: {
   reset(){
     this.CategoryPage = true
     this.SearchPage = false
   },
   async getResult(query){  
        console.log(query) 
        this.moviequery = query
        axios.defaults.headers.post['Access-Control-Allow-Origin'] = '*';
        await axios.get('http://api.themoviedb.org/3/search/tv?api_key=f954acb98066979df324be00ad15738a&query=' + query + '&callback=test').then(response => { 
            const l = response.data.length
            const a = response.data.substr(5,l-6)
            this.results = JSON.parse(a).results.filter((i)=> {return i.poster_path!==null })
        })
        this.SearchPage = true
        this.CategoryPage = false
        console.log(this.results) 
    }
  },
  
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
.posterimage{
    height:380px; 
  width:256px; 
  border-radius: 16px;
}
.posterimage:hover{
  cursor: pointer;
}
</style>
