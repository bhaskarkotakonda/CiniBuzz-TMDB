<template>
    <div @click="$emit('gotoCategory')" class="TopDiv">
        <span class="topname" style="color: #6855D6 position: absolute; left: 20%;  
    top: 5%;
    font: Baloo Bhai;
    font-style: normal;
    font-weight: normal;
    font-size: 40px;
    line-height: 57px;"> CiniBuzz</span>
    </div>
</template>


<script>
export default {
    name: 'TopHeader',

}
</script>

<style scoped>
.TopDiv{
    max-width:1040px;
}
.TopDiv:hover{
    cursor:pointer
}
.topname{
    position: absolute;
    left: 0%;
    right: 89.62%;
    top: 5%;
    bottom: -35.71%;
    font-family: Baloo Bhai;
    font-style: normal;
    font-weight: normal;
    font-size: 36px;
    line-height: 57px;
    color: #6855D6 !important;
    
}

</style>
