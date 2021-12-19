<template>
    <div>
        <div style="top: 520px; margin-left:178px; margin-right:178px; width:1288px; height:200px; position:absolute">
            <p align="left" style="font-family: Inter; font-style: normal; font-weight: normal; font-size: 40px; line-height: 48px; color: #000000;">Browse movies by category</p>
            <div style="display:flex; flex-direction:vertical flex-wrap: nowrap; align-content: space-between;align-items: baseline; justify-content: space-evenly;">
                <CategoryBox @updateCategory="update" v-for="category in cats" :key="category" v-bind:category="category" :selectedCategory="selectedCategory"></CategoryBox>
            </div>
        </div>
        <div style="top:702px; position:absolute; margin-left: 178px; margin-right: 178px; width: 1288px; height: 1300px; display:flex; flex-basis:25%; flex-direction: row; flex-wrap: wrap; align-content: space-between;align-items: baseline; justify-content: space-between;">
            <div v-for='result in entries' :key='result.id'>
                <div style="margin-right:5px;" v-if="result.poster_path">
                <img class="posterimage"  v-bind:src="'http://image.tmdb.org/t/p/w500/' +    result.poster_path" >
                <p  align="left" style="max-width:250px; font-family: Inter;font-style: normal;font-weight: 600;font-size: 20px;line-height: 24px;">{{result.original_title}}</p>
                </div>
            </div>
        </div>
    </div>
</template>


<script>
import CategoryBox from './CategoryBox'
import axios from 'axios'
export default {
    name: 'CategoryBar',
    props: ['categories'],
    components: {CategoryBox},
    mounted() {
        this.update('Upcoming')
    },
    data() {
        return{
            cats: this.categories,
            selectedCategory: 'Upcoming',
            entries: []
        }
    },
    methods: {
        async update(cat){
            this.selectedCategory = cat
            console.log(cat)
            axios.defaults.headers.post['Access-Control-Allow-Origin'] = '*';
            if(cat==='Drama'){
               await axios.get('https://api.themoviedb.org/3/discover/movie?api_key=f954acb98066979df324be00ad15738a&with_genres=28&callback=test').then(response => { 
                    const l = response.data.length
                    const a = response.data.substr(5,l-6)
                    this.entries = JSON.parse(a).results.filter((i)=> {return i.backdrop_path!==null })
                }) 
            }
            else if(cat==='Thriller'){
               await axios.get('https://api.themoviedb.org/3/discover/movie?api_key=f954acb98066979df324be00ad15738a&with_genres=35&callback=test').then(response => { 
                    const l = response.data.length
                    const a = response.data.substr(5,l-6)
                    this.entries = JSON.parse(a).results.filter((i)=> {return i.backdrop_path!==null })
                }) 
            }
            else{
                await axios.get('https://api.themoviedb.org/3/movie/' + cat.toLowerCase() + '?api_key=f954acb98066979df324be00ad15738a&language=en-US').then(response => { 
                    console.log(response)
                    const a = response.data
                    this.entries = a.results.filter((i)=> {return i.backdrop_path!==null })
                })
            }            
            console.log(this.entries) 
        }
    }
}
</script>
