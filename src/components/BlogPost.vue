<script setup>
    //defineProps(['title','id','body','ColorText'])
    defineProps({
        title: String,
        id: Number,
        body: {
            type: String,
            default: 'Sin descripción',
        },
    });

    const emit = defineEmits(['cambiarFavoritoNombre']);
</script>

<template>
    <div class="card">
      <div class="card-body">
        <h5 style="color:black" class="card-title">{{ id }} - {{ title }}</h5>
        <p style="color:black">{{ body }}</p>
        <button @click="emit('cambiarFavoritoNombre',id)" class="btn btn-outline-primary">Favorito</button>
      </div>
    </div>
  </template>