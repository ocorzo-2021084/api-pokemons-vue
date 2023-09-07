
<script setup>
import { useRoute, useRouter } from 'vue-router';
import { useGetData } from '@/composables/getData';

const route = useRoute();
const router = useRouter();

const back = () => {
    router.push('/pokemons');
}

const { data, getData, loading, error } = useGetData();

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);

</script>
<template>
    <p v-if="loading">Carcando informacion</p>
    <div class="alert alert-danger" v-if="error">
        {{ error }}
    </div>
    <div v-if="data">
        <img :src="data.sprites?.front_default" alt="">
        <h1>Poke name: {{ $route.params.name }}</h1>
    </div>
    <h1 v-else>No existe el pokemon</h1>
    <button @click="back" class="btn btn-primary">Volver</button>
</template>