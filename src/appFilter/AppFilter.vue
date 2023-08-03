<template >
    <div class="btn-group">
        <button class="btn" @click="filterHandler('all')" :class="[filterName === 'all' ? 'btn-dark' : 'btn-btn-outline-dark']">Barcha kinolar</button>
        <button class="btn" @click="filterHandler('popular')" :class="[filterName === 'popular' ? 'btn-dark' : 'btn-btn-outline-dark']">Mashhur kinolar</button>
        <button class="btn" @click="filterHandler('mostViewers')" :class="[filterName === 'mostViewers' ? 'btn-dark' : 'btn-btn-outline-dark']">Eng ko'p ko'rilgan kinolar</button>
    </div>
</template>
<script>
export default {
   props:{
    updateFilterHandler:{
        type:Function,
        required:true
    },
    filterName:{
        type:String,
        required:true
    }
   },
   data(){
    return {
        filter:'all'
    }
   },
   methods:{
    filterHandler(filter){
        this.filter = filter
        this.updateFilterHandler(this.filter)
    }
   }
}
</script>
<style ></style>