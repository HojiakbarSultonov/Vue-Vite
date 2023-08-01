<template>
    <div class="movie-add-form">
        <h3>Yangi kino qo'shish</h3>
        <form action="" class="add-form d-flex">
            <input type="text" placeholder="Qanday kino?" class="form-control new-movie-label">
            <input type="text" placeholder="Necha marta ko'rilgan?" class="form-control new-movie-label">
            <button class="btn-outline-dark" type="submit">Qo'shish</button>
        </form>
    </div>
</template>
<script>
export default {

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