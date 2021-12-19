<template>
    <button @click="$emit('updateCategory',category)" :style="{opacity:(selectedCategory===category)?1:0.54}" style="border:0.5px; font-family: Inter; font-style: normal; font-weight: normal; font-size: 20px; line-height: 24px; color: #000000; background: #F7F7F7; border-radius: 8px;"> 
        {{category}}
    </button>
</template>


<script>
export default {
    name: 'CategoryBox',
    props: ['category','selectedCategory'],
    data() {
        return{
            
        }
    }
}
</script>

<style scoped>
.categorybutton:hover{
    
}
</style>