<script setup>
import {RouterLink} from 'vue-router';
import { useFavoritosStore } from '@/store/favoritos';
import { storeToRefs } from 'pinia';

const useFavoritos = useFavoritosStore();

const { favoritos } = storeToRefs(useFavoritos)
const { remove } = useFavoritos;

</script>
<template>
    <h1>Favoritos</h1>
    <p v-if="favoritos.length == 0">Sin favoritos...</p>
    <ul class="list-group list-group-flush">
        <li class="list-group-item" v-for="poke in favoritos" :key="poke.id">
            <div>
                {{ poke.name }}
            </div>
            <div>
                <button class="btn btn-danger mb-2" @click="remove(poke.id)">Eliminar</button>
            </div>
            <div>
                <RouterLink class="btn btn-primary " :to="`/pokemons/${poke.name}`">Mas informacion</RouterLink>
            </div>
        </li>
    </ul>
</template>