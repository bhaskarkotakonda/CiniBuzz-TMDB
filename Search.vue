<template>
  <div class="search" style="border-radius: 16px;background: #F2F1F8; margin-left:178px; margin-right:178px;  height:375px; position:absolute">
    <p style="margin-top:100px; margin-left:400px; position:absolute; font-family: Inter; font-style: normal; font-weight: normal; font-size: 40px; line-height: 48px; color: #000000;"> Find perfect movie for <strong>evening</strong> </p>
    <div style = "position:relative; margin:218px 216px 101px 92px; height:56px; width:980px; ">
    <input id="inp" type='text' style="border-color:#FFFFFF;height:56px; width:786px; background: #FFFFFF; border-radius: 12px;" v-model='query' @keyup.enter='sendRequest(query)'>
    <button  style="border-color:#FFFFFF; position:relative; left:20px; width: 126px; height: 56px; background:rgba(104, 85, 214, 0.54);  border-radius: 12px;"  @click='sendRequest(query)'> 
      <span class="searchbutton" style= "font-family: Inter; font-style: normal; font-weight: bold;  font-size: 16px; line-height: 19px; color: #FFFFFF; opacity: 0.5;" >
        SEARCH
      </span>
      </button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'search',
  props: ['moviequery'],
  data () {
    return {
        query: this.moviequery,
    }
  },
  methods: {
    sendRequest(query){
      this.$emit("getResult",query);
      this.query = null
      document.getElementById('inp').blur()
    }
  }
}
</script>

<style>
.button:hover{
  cursor: pointer
}
</style>