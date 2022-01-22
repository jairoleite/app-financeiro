<template>
  <q-layout view="lHh Lpr lFf">
    <q-footer bordered class="bg-white text-primary">
      <q-tabs
        no-caps
        active-color="primary"
        indicator-color="transparent"
        class="text-grey"
        v-model="tab"
      >
        <EssentialLink
          v-for="(link, index) in essentialLinks"
          :key="index"
          v-bind="link"
        />
        <!-- tab para sair da aplicação -->
        <q-tab icon="logout" @click="handleLogout" />
      </q-tabs>
    </q-footer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from "components/EssentialLink.vue";

const linksList = [
  {
    icon: "home",
    routeName: "me",
  },
  {
    icon: "settings",
    routeName: "config",
  },
];

import { defineComponent, ref } from "vue";
import useAuthUser from "src/composables/UseAuthUser";
import { useRouter } from "vue-router";
import { useQuasar } from "quasar";

export default defineComponent({
  name: "MainLayout",

  components: {
    EssentialLink,
  },

  setup() {
    // rotas
    const router = useRouter();
    //pega página atual
    const tab = ref(router.currentRoute.value.name);
    //  componentes quasar
    const $q = useQuasar();
    //logout do usuário
    const { ogout } = useAuthUser();

    const handleLogout = async () => {
      $q.dialog({
        title: "Já vai :(",
        message: "Deseja realmente sair ?",
        cancel: true,
        persistent: true,
      })
        .onOk(async () => {
          await logout();
          router.replace({ name: "login" });
        })
        .onCancel(async () => {
          tab.value = router.currentRoute.value.name;
        });
    };

    return {
      tab,
      essentialLinks: linksList,
      handleLogout,
    };
  },
});
</script>
