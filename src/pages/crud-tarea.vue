<template>
  <div class="text-underline q-mb-md">{{ titulo }}</div>

  <div class="row">
    <div class="q-px-md col-6 q-pr-xl" style="max-width: 300px">
      <q-form @submit="submitTarea()">
        <q-input
          class="q-mb-md"
          outlined
          dense
          v-model="tarea.titulo"
          label="Titulo de la tarea"
          lazy-rules
          :rules="[
            (val) => (val !== null && val !== '') || 'El campo es obligatorio',
          ]"
        />

        <q-input
          class="q-mb-md"
          outlined
          dense
          v-model="tarea.descripcion"
          label="Descripción de la tarea"
          lazy-rules
          :rules="[
            (val) => (val !== null && val !== '') || 'El campo es obligatorio',
          ]"
        />

        <div>
          <q-btn
            :label="editIndice !== null ? 'Editar' : 'Enviar'"
            class="float-right"
            type="submit"
            :color="editIndice !== null ? 'yellow-14' : 'green'"
            :icon="editIndice !== null ? 'mdi-content-save-alert' : 'mdi-send'"
          />
        </div>
      </q-form>
    </div>

    <div class="col-6">
      <TareaVistaPrevia
        :titulo="tarea.titulo"
        :descripcion="tarea.descripcion"
      />
    </div>
  </div>

  <div class="row q-ml-md q-mt-xl">
    <template v-for="({ titulo, descripcion }, i) in listaTareas" :key="titulo">
      <div class="col-3 q-pr-md">
        <ListTareas
          :titulo="titulo"
          :descripcion="descripcion"
          :indice="i"
          @delete-tarea="deleteTareaFn"
          @edit-tarea="editTareaFn"
        >
          <template #footer>
            <q-separator dark inset />
            <div class="q-pa-md text-center">
              <div class="text-h5 q-mb-lg">Slot footer</div>
              <div><b>El numero de indice es:</b> {{ i }}</div>
            </div>
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

const titulo = ref("Page PRUEBA");
const editIndice = ref(null);

const tarea = ref({
  titulo: "",
  descripcion: "",
});

const listaTareas = ref([]);

const submitTarea = () => {
  console.log(tarea.value);

  //Para editar la tarea
  if (editIndice.value !== null) {
    listaTareas.value[editIndice.value].titulo = tarea.value.titulo;
    listaTareas.value[editIndice.value].descripcion = tarea.value.descripcion;
    editIndice.value = null;
    tarea.value.titulo = "";
    tarea.value.descripcion = "";
    return;
  } //Fin editar tarea

  listaTareas.value.push({
    titulo: tarea.value.titulo,
    descripcion: tarea.value.descripcion,
  });

  tarea.value.titulo = "";
  tarea.value.descripcion = "";

  console.log(listaTareas.value);
};

const deleteTareaFn = (indice) => {
  listaTareas.value.splice(indice, 1);
};

const editTareaFn = (t) => {
  console.log(t);

  tarea.value.titulo = t.titulo;
  tarea.value.descripcion = t.descripcion;
  editIndice.value = t.indice;
  console.log(editIndice.value);
};
</script>


<style lang="sass" scoped></style>