<template>
        <div v-if="result.poster_path">
            <p>{{result.name}}</p>
            <img v-bind:src="'http://image.tmdb.org/t/p/w500/' +    result.poster_path" width='100px'>
        </div>
</template>

<script>

export default {
    name: 'CardItem',
    props: ['result'],
}
</script>