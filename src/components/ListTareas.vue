<template>
  <q-card dark bordered class="bg-grey-9 my-card q-mb-xl">
    <q-card-section class="row justify-between">
      <div class="text-h6">{{ titulo }}</div>
      <div>
        <q-btn
          flat
          color="yellow-14"
          padding="xs"
          icon="edit"
          @click="
            $emit('edit-tarea', {
              titulo: titulo,
              descripcion: descripcion,
              indice: indice,
            })
          "
        />
        <q-btn
          flat
          padding="xs"
          color="white"
          icon="close"
          @click="$emit('delete-tarea', indice)"
        />
      </div>
    </q-card-section>

    <q-separator dark inset />

    <q-card-section>
      {{ descripcion }}
    </q-card-section>

    <slot name="footer" />
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
  indice: {
    type: Number,
    required: true,
  },
});

const emit = defineEmits(["delete-tarea", "edit-tarea"]);
</script>

<style lang="sass" scoped>
.my-card
  max-width: 300px
</style>