<template>
  <q-page padding>
    <!-- topo -->
    <q-toolbar>
      <q-avatar class="q-mt-md q-mr-sm" size="50px">
        <q-img
          src="~/assets/perfil.png"
          spinner-color="primary"
          spinner-size="50px"
        />
      </q-avatar>

      <span class="text-primary">Olá, {{ user.user_metadata.name }}!</span>
    </q-toolbar>
    <!-- fim -->

    <!-- resumo de gastos -->
    <div class="row">
      <h6>gasto</h6>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import useAuthUser from "src/composables/UseAuthUser";

export default defineComponent({
  name: "PageMe",
  setup() {
    const { user } = useAuthUser();

    return {
      user,
    };
  },
});
</script>
