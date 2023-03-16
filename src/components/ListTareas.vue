<template>
  <q-card dark bordered class="bg-grey-9 q-mx-md q-mt-xl my-card text-white">
    <q-card-section>
      <div class="text-h6">
        {{ nombre }}
        <q-btn
          @click="$emit('delete-tarea', indice)"
          dense
          class="float-right"
          round
          flat
          color="white"
          icon="mdi-window-close"
        />
      </div>
    </q-card-section>

    <q-card-section class="q-py-none">
      {{ descripcion }}
    </q-card-section>

    <q-card-section>
      <slot name="footer"></slot>
    </q-card-section>
  </q-card>
</template>

<script setup>
const emit = defineEmits(["delete-tarea"]);
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
  indice: {
    type: Number,
    required: true,
  },
});
</script>

<style lang="sass" scoped>
.my-card
    width: 100%
    max-width: 350px
</style>