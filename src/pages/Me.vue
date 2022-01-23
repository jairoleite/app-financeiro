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

      <span class="text-primary">Olá, {{ userName }}!</span>
    </q-toolbar>
    <!-- fim -->

    <!-- resumo de gastos -->
    <div class="row q-mx-md q-my-md">
      <q-card class="card-resumo">
        <q-card-section>
          <div class="text-h6">Resumo</div>
          <div class="text-subtitle2">
            <span> Data: 22/01/2022 </span>
          </div>
        </q-card-section>
        <q-card-section style="margin-top: -20px">
          <!-- receitas -->
          <div class="values">
            <q-icon
              class="q-mr-sm color-receita"
              size="30px"
              name="arrow_circle_up"
            />
            <span class="text-bold color-receita"
              ><b class="q-mr-sm"> Receita: </b>
              R$ 1.500,00
            </span>
            <!-- <q-btn class="color-receita" flat round icon="visibility" /> -->
          </div>
          <!-- fim -->

          <!-- dispesas -->
          <div class="values">
            <q-icon
              class="q-mr-sm color-despesa"
              size="30px"
              name="arrow_circle_down"
            />
            <span class="text-bold color-despesa"
              ><b class="q-mr-sm"> Dispesa: </b>
              R$ 500,00
            </span>
            <!-- <q-btn class="color-despesa" flat round icon="visibility" /> -->
          </div>
          <!-- fim -->
        </q-card-section>
      </q-card>
    </div>

    <!-- últimos lançamentos -->
    <div class="row q-mx-md q-mt-xl">
      <span class="text-primary">Últimos lançamentos</span>

      <!-- lançamento -->
      <q-card class="card-lancamento shadow-7">
        <q-card-section>
          <q-item>
            <q-item-section avatar>
              <q-icon color="blue" name="shopping_cart" />
            </q-item-section>
            <q-item-section>
              <q-item-label>Supermercado</q-item-label>
              <q-item-label caption lines="2">compras do mês </q-item-label>
            </q-item-section>
            <q-item-section side>
              <q-item-label caption>R$ 550,00</q-item-label>
            </q-item-section>
          </q-item>
        </q-card-section>
      </q-card>

      <q-card class="card-lancamento shadow-7">
        <q-card-section>
          <q-item>
            <q-item-section avatar>
              <q-icon color="red" name="cottage" />
            </q-item-section>
            <q-item-section>
              <q-item-label>Supermercado</q-item-label>
              <q-item-label caption lines="2"
                >despesas com a casa compra de espelho
              </q-item-label>
            </q-item-section>
            <q-item-section side>
              <q-item-label caption>R$ 180,00</q-item-label>
            </q-item-section>
          </q-item>
        </q-card-section>
      </q-card>
      <!-- fim -->
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";
import useAuthUser from "src/composables/UseAuthUser";

export default defineComponent({
  name: "PageMe",
  setup() {
    // autenticação do usuário
    const { user } = useAuthUser();
    //userName
    const userName = ref("");
    if (user.value.user_metadata) {
      userName.value = user.value.user_metadata.name;
    }

    return {
      userName,
    };
  },
});
</script>

<style scoped>
.card-resumo {
  color: aliceblue;
  width: 100%;
  border-radius: 12px;
  background: #50a3a2;
  background: linear-gradient(to bottom right, #50a3a2 0%, #53e3a6 100%);
}

.card-resumo .values {
  display: flex;
  align-items: center;
}

.card-resumo .color-receita {
  color: #0000c7;
}

.card-resumo .color-despesa {
  color: #c40045;
}

.card-lancamento {
  width: 100%;
  margin-top: 8px;
  border-radius: 14px;
}
</style>
