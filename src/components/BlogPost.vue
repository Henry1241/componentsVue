<script setup>
//const props = defineProps(["title", "id", "body", "colorText"]);
//console.log(props.title);
//console.log(props.id);
defineProps({
    title: String,
    id: Number,
    body: {
        type: String,
        default: "Sin descripcion",
    },
})

const emit =defineEmits(['changeFavoriteName'])

//emit('changeFavoriteName', title)
</script>

<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">
        {{ id }} - {{ title }}
      </h5>
      <p>{{ body }}</p>
      <button @click="$emit('changeFavoriteName', title)" 
              class="btn btn-outline primary">Favorito</button>
    </div>
  </div>
</template>
