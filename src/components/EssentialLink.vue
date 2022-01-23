<template>
  <q-tab :name="routeName" :icon="icon" @click="clickTab">
    <span>{{ label }}</span>
  </q-tab>
</template>

<script>
import { defineComponent } from "vue";
import { useRouter } from "vue-router";

export default defineComponent({
  name: "EssentialLink",
  props: {
    routeName: {
      type: String,
      default: "",
    },

    icon: {
      type: String,
      default: "",
    },

    label: {
      type: String,
      default: "",
    },
  },

  setup(props) {
    const router = useRouter();

    // redireciona para página
    const clickTab = () => {
      router.push({ name: props.routeName });
    };

    return { clickTab };
  },
});
</script>
