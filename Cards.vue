<template>
    <div style="top:720px; position:absolute; margin-left: 178px;
    margin-right: 178px;
    width: 1288px;
    height: 800px;">
        <div v-for='result in sentresults' :key='result.id'>
            <p>{{result.name}}</p>
            <img v-bind:src="'http://image.tmdb.org/t/p/w500/' +    result.poster_path" width='100px'>
        </div>
    </div>
</template>

<script>

export default {
    name: 'Cards',
    props: ['results'],    
    computed: {
        results() {
            console.log(this.results)
            return this.results
        } 
    },
    mounted() {
        console.log(this.results)
    },
    data() {
        return {
            sentresults: this.results,
        }
    }
}
</script>
