<template lang="">
   <input type="text" placeholder="Kinolarni qidirish" class="form-control search-input" @input = "changeHandler" :value = "term">
</template>
<script>
export default {
   props:{
      updateTermHandler:{
         type:Function,
         required:true
      }
   },
   date(){
      return {
         term:''
      }
   },

   methods: {
      changeHandler(e){
         this.term = e.target.value
         this.updateTermHandler(this.term)
      }
   },
}
</script>
<style scoped>
.search-input {
    margin-bottom: 1rem ;
    padding: 1.5rem;
    background:#fcfef5;
    border-radius: 4px;
     box-shadow: 15px 15px 15px rgba(0,0,0,0.15);
}
</style>