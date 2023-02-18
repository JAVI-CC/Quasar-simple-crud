<template>
  <q-card
    class="my-card text-white"
    style="background: radial-gradient(circle, #35a2ff 0%, #014a88 100%)"
  >
    <q-card-section>
      <div class="text-h6" v-if="titulo !== ''">{{ titulo }}</div>
      <div class="text-h6" v-else>Escribe un titulo...</div>
    </q-card-section>

    <q-card-section class="q-pt-none" v-if="descripcion !== ''">
      {{ descripcion }}
    </q-card-section>
    <q-card-section class="q-pt-none" v-else
      >Escribe una descripción...</q-card-section
    >
  </q-card>
</template>

<script setup>
const props = defineProps({
  titulo: {
    type: String,
    required: true,
    default: "{{ Titulo }}",
  },
  descripcion: {
    type: String,
    required: true,
    default: "{{ Descripción }}",
  },
});
</script>

<style lang="sass" scoped>
.my-card
    max-width: 300px
</style>