<template>
  <q-page padding class="flex flex-center wrapper">
    <q-form
      class="row justify-center container"
      @submit.prevent="handleRegister"
    >
      <p class="col-12 text-h5 text-center text-white">Registre-se</p>
      <div
        style="width: 100%; max-width: 290px !important"
        class="q-gutter-y-md"
      >
        <q-input
          label="Nome"
          input-style="color: #0b4645; "
          color="white"
          label-color="white"
          v-model="form.name"
          lazy-rules
          :rules="[(val) => (val && val.length > 0) || 'Nome obrigatório']"
        />

        <q-input
          label="E-mail"
          input-style="color: #0b4645; "
          color="white"
          label-color="white"
          v-model="form.email"
          lazy-rules
          :rules="[(val) => (val && val.length > 0) || 'E-mail obrigatório']"
          type="email"
        />

        <q-input
          label="Senha"
          input-style="color: #0b4645; "
          color="white"
          label-color="white"
          v-model="form.password"
          type="password"
          lazy-rules
          :rules="[
            (val) =>
              (val && val.length >= 6) ||
              'A senha é obrigatório e pode conter no mínimo 6 caracteres',
          ]"
        />

        <div class="full-width q-pt-md q-gutter-y-sm">
          <q-btn
            label="registrar"
            color="white"
            class="full-width"
            outline
            rounded
            type="submit"
          />

          <q-btn
            label="voltar"
            color="white"
            class="full-width"
            rounded
            flat
            :to="{ name: 'login' }"
          />
        </div>
      </div>
    </q-form>

    <ul class="bg-bubbles">
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ul>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";
import useAuthUser from "src/composables/UseAuthUser";
import useNotify from "src/composables/UseNotify";
import { useRouter } from "vue-router";

export default defineComponent({
  name: "PageRegister",

  setup() {
    const router = useRouter();
    const { register } = useAuthUser();
    const { notifyError, notifySuccess } = useNotify();

    const form = ref({
      name: "",
      email: "",
      password: "",
    });

    const handleRegister = async () => {
      try {
        await register(form.value);
        notifySuccess();
        router.push({
          name: "email-confirmation",
          query: { email: form.value.email },
        });
      } catch (error) {
        notifyError(error.message);
      }
    };

    return {
      form,
      handleRegister,
    };
  },
});
</script>

<style scoped>
.wrapper {
  background: #50a3a2;
  background: linear-gradient(to bottom right, #50a3a2 0%, #53e3a6 100%);
  position: absolute;
  width: 100%;
  overflow: hidden;
}
.container {
  margin: 0 auto;
  padding: 80px 0;
  text-align: center;
  z-index: 10;
}
.bg-bubbles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
.bg-bubbles li {
  position: absolute;
  list-style: none;
  display: block;
  width: 40px;
  height: 40px;
  background-color: rgba(255, 255, 255, 0.15);
  bottom: -160px;
  -webkit-animation: square 25s infinite;
  animation: square 25s infinite;
  transition-timing-function: linear;
}
.bg-bubbles li:nth-child(1) {
  left: 10%;
}
.bg-bubbles li:nth-child(2) {
  left: 20%;
  width: 80px;
  height: 80px;
  -webkit-animation-delay: 2s;
  animation-delay: 2s;
  -webkit-animation-duration: 17s;
  animation-duration: 17s;
}
.bg-bubbles li:nth-child(3) {
  left: 25%;
  -webkit-animation-delay: 4s;
  animation-delay: 4s;
}
.bg-bubbles li:nth-child(4) {
  left: 40%;
  width: 60px;
  height: 60px;
  -webkit-animation-duration: 22s;
  animation-duration: 22s;
  background-color: rgba(255, 255, 255, 0.25);
}
.bg-bubbles li:nth-child(5) {
  left: 70%;
}
.bg-bubbles li:nth-child(6) {
  left: 80%;
  width: 120px;
  height: 120px;
  -webkit-animation-delay: 3s;
  animation-delay: 3s;
  background-color: rgba(255, 255, 255, 0.2);
}
.bg-bubbles li:nth-child(7) {
  left: 32%;
  width: 160px;
  height: 160px;
  -webkit-animation-delay: 7s;
  animation-delay: 7s;
}
.bg-bubbles li:nth-child(8) {
  left: 55%;
  width: 20px;
  height: 20px;
  -webkit-animation-delay: 15s;
  animation-delay: 15s;
  -webkit-animation-duration: 40s;
  animation-duration: 40s;
}
.bg-bubbles li:nth-child(9) {
  left: 25%;
  width: 10px;
  height: 10px;
  -webkit-animation-delay: 2s;
  animation-delay: 2s;
  -webkit-animation-duration: 40s;
  animation-duration: 40s;
  background-color: rgba(255, 255, 255, 0.3);
}
.bg-bubbles li:nth-child(10) {
  left: 90%;
  width: 160px;
  height: 160px;
  -webkit-animation-delay: 11s;
  animation-delay: 11s;
}
@-webkit-keyframes square {
  0% {
    transform: translateY(0);
  }
  100% {
    transform: translateY(-700px) rotate(600deg);
  }
}
@keyframes square {
  0% {
    transform: translateY(0);
  }
  100% {
    transform: translateY(-700px) rotate(600deg);
  }
}
</style>
