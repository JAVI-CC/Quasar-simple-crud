<template>
  <q-card
    class="q-mx-md q-mt-xl my-card text-white"
    style="background: radial-gradient(circle, #35a2ff 0%, #014a88 100%)"
  >
    <q-card-section>
      <div class="text-h6">
        {{ nombre !== "" ? nombre : "{ Nombre }" }}
      </div>
    </q-card-section>

    <q-card-section class="q-pt-none">
      {{ descripcion !== "" ? descripcion : "{ Descripción }" }}
    </q-card-section>
  </q-card>
</template>

<script setup>
const props = defineProps({
  nombre: {
    type: String,
    required: true,
    default: "",
  },
  descripcion: {
    type: String,
    required: true,
    default: "",
  },
});
</script>

<style lang="sass" scoped>
.my-card
    width: 100%
    max-width: 350px
</style>