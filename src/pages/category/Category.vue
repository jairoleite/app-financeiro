<template>
  <q-page padding>
    <!-- topo -->
    <q-toolbar class="q-mb-md">
      <q-toolbar-title class="text-primary text-center">
        Cadastro de categoria
      </q-toolbar-title>
    </q-toolbar>
    <!-- fim -->
    <div class="row">
      <q-table
        :rows="categories"
        :columns="columns"
        row-key="id"
        class="col-12"
        :loading="loading"
      >
        <template v-slot:top>
          <q-btn
            icon="add"
            color="primary"
            dense
            label="Adicionar"
            no-caps
            @click="modalCategory = true"
          />
        </template>
        <template v-slot:body-cell-actions="props">
          <q-td :props="props" class="q-gutter-x-sm">
            <q-btn icon="edit" color="info" dense size="sm">
              <q-tooltip> Editar </q-tooltip>
            </q-btn>
            <q-btn icon="delete" color="negative" dense size="sm">
              <q-tooltip> Deletar </q-tooltip>
            </q-btn>
          </q-td>
        </template>
      </q-table>
    </div>

    <!-- poupap de criação da categoria -->
    <q-dialog v-model="modalCategory" persistent>
      <q-card style="min-width: 350px">
        <q-card-section>
          <div class="text-primary text-h6">Adicionar nova categoria</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <q-input dense autofocus label="Nome" />
        </q-card-section>

        <span class="q-ml-md text-gray">Selecione um ícone:</span>
        <q-card-section class="row q-pt-none">
          <div v-for="(icon, index) in icons" :key="index">
            <q-radio
              class="q-mx-sm"
              v-model="seletectedIcon"
              @update:model-value="updateIcon"
              :val="icon.name"
            >
              <q-icon size="25px" :name="icon.name" />
            </q-radio>
          </div>
        </q-card-section>

        <q-card-actions align="right" class="text-primary">
          <q-btn flat label="Cancel" v-close-popup />
          <q-btn color="primary" label="Salvar" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>
    <!-- fim -->
  </q-page>
</template>

<script>
// configurações da tabela de categoria
const columns = [
  { name: "nome", align: "left", label: "Nome", field: "nome", sortable: true },
  {
    name: "actions",
    align: "right",
    label: "Ações",
    field: "actions",
  },
];

const icons = [
  { name: "cottage" },
  { name: "credit_card" },
  { name: "savings" },
  { name: "monetization_on" },
  { name: "directions_car" },
  { name: "local_mall" },
  { name: "local_gas_station" },
  { name: "construction" },
  { name: "two_wheeler" },
  { name: "favorite" },
  { name: "psychology" },
  { name: "engineering" },
  { name: "shopping_cart" },
];

import { defineComponent, ref, onMounted } from "vue";
import useApi from "src/composables/UseApi";
import useNotify from "src/composables/UseNotify";

export default defineComponent({
  name: "PageCategoryList",
  setup() {
    // lista de categorias
    const categories = ref([]);
    // icone da categoria
    const seletectedIcon = ref(null);
    // loading da lista
    const loading = ref(true);

    // modal da categoria
    const modalCategory = ref(true);

    const { list } = useApi();
    const { notifyError } = useNotify();

    // carrega listagem do banco
    const handleListCategories = async () => {
      try {
        loading.value = true;
        categories.value = await list("categoria_lancamento");
        loading.value = false;
      } catch (error) {
        notifyError(error.message);
      }
    };

    const updateIcon = (value) => {
      console.log(value);
    };

    onMounted(() => {
      handleListCategories();
    });

    return {
      columns,
      categories,
      loading,
      modalCategory,
      icons,
      seletectedIcon,
      updateIcon,
    };
  },
});
</script>