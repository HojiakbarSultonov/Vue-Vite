<template>
    <div class="movie-add-form">
        <h3>Yangi kino qo'shish</h3>
        <form action="" class="add-form d-flex" @submit.prevent>
            <input type="text" placeholder="Qanday kino?" class="form-control new-movie-label" :value="name"
                @input="name = $event.target.value">
            <input type="number" placeholder="Necha marta ko'rilgan?" class="form-control new-movie-label" :value="viewers"  @input="viewers = $event.target.value">
            <button class="btn-outline-dark" type="submit" @click="addMovie">Qo'shish</button>
        </form>
    </div>
</template>
<script>
export default {
    data() {
        return {
            name: '',
            viewers: '',
        }
    },
    methods:{
        addMovie(){
            // e.preventDefault();
            
            const newMovie = {
                name: this.name,
                viewers:this.viewers,
                favourite:false,
                like:false,
                id:Date.now()
            }
            this.$emit('createMovie', newMovie)
            this.name = "",
            this.viewers = ""
        }
    }

}
</script>
<style >
.movie-add-form {
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>