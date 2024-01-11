<script setup>
defineProps(["inicio", "fin", "maxLength"])
const emit = defineEmits(['next', 'prev'])

const activeNext = () => {
  console.log("Pasaste a la siguente pagina");
  emit("next");
};
</script>

<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button
      @click="$emit('prev')"
      type="button"
      class="btn btn-outline-primary"
      :disabled="inicio <= 0"
    >
      Previous {{ inicio }}
    </button>
    <button
      @click="activeNext"
      type="button"
      class="btn btn-outline-primary"
      :disabled="fin >= maxLength"
    >
      Next {{ fin  }}
    </button>
  </div>
</template>
