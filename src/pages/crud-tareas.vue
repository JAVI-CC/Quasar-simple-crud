<template>
  <div class="row">
    <div class="col-4">
      <q-form @submit.prevent="onSubmitTarea" class="q-ma-md q-gutter-md">
        <div class="text-h6">Formulario para crear tarea</div>

        <q-input
          outlined
          dense
          v-model="tarea.nombre"
          label="Nombre"
          lazy-rules
          :rules="[(val) => !!val || 'Debes rellenar este campo']"
        />

        <q-input
          outlined
          dense
          v-model="tarea.descripcion"
          label="Descripción"
          lazy-rules
          :rules="[(val) => !!val || 'Debes rellenar este campo']"
        />

        <div>
          <q-btn
            class="float-right"
            label="Guardar"
            icon-right="mdi-content-save"
            type="submit"
            color="positive"
          />
        </div>
      </q-form>
    </div>

    <div class="col-8">
      <TareaVistaPrevia
        :nombre="tarea.nombre"
        :descripcion="tarea.descripcion"
      />
    </div>

    <template v-for="({ nombre, descripcion }, i) in tareas" :key="nombre">
      <div class="col-3">
        <ListTareas
          :nombre="nombre"
          :descripcion="descripcion"
          :indice="i"
          @delete-tarea="onDeleteTarea"
        >
          <template #footer>
            <q-separator color="white" class="q-mb-sm q-pr-md" />
            El numero del indice es: {{ i }}
          </template>
        </ListTareas>
      </div>
    </template>
  </div>
</template>

<script setup>
import { ref } from "vue";
import TareaVistaPrevia from "../components/TareaVistaPrevia.vue";
import ListTareas from "../components/ListTareas.vue";

const tarea = ref({
  nombre: "",
  descripcion: "",
});

const tareas = ref([]);

const onSubmitTarea = () => {
  tareas.value.push(tarea.value);
  tarea.value = [
    {
      nombre: "",
      descripcion: "",
    },
  ];
};

const onDeleteTarea = (i) => {
  tareas.value.splice(i, 1);
  console.log(i);
};
</script>

<style lang="sass" scoped>
</style>