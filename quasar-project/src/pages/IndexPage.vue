<template>
  <q-page class="bg-cover bg-center column items-center justify-center q-pa-md" :style="backgroundStyle">
    <div
      class="column items-center justify-center q-gutter-md text-white text-center"
      style="width: 100%; max-width: 800px;"
    >
      <!-- Apresentação do projeto -->
      <div v-if="!mostrarFormulario">
        <h1 class="text-h4 q-mb-md">
          Bem-vindo ao Canal de Denúncia Anônima contra a Violência Doméstica
        </h1>

        <p class="text-subtitle1">
          Este espaço foi criado para oferecer um ambiente seguro, sigiloso e acessível a todos que desejam denunciar situações de violência doméstica sem se identificar.
        </p>

        <p class="text-subtitle1">
          A violência doméstica pode se manifestar de diversas formas: física, psicológica, sexual, moral ou patrimonial. Nenhuma delas deve ser ignorada. Seu relato pode salvar vidas.
        </p>

        <p class="text-subtitle1">
          Todas as informações enviadas são tratadas com seriedade e encaminhadas para instituições responsáveis, respeitando o sigilo e a integridade dos envolvidos.
        </p>

        <p class="text-subtitle1 q-mb-md">
          <strong>Se você está em risco imediato, ligue 190. Para orientação, disque 180.</strong>
        </p>

        <q-btn
          label="Fazer denúncia anônima"
          color="negative"
          size="lg"
          class="q-mt-md"
          @click="mostrarFormulario = true"
        />
      </div>

      <!-- Formulário aparece quando mostrarFormulario = true -->
      <FormComponent v-if="mostrarFormulario" />
    </div>
  </q-page>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import FormComponent from 'components/Form.vue'
import bgImage from '../assets/cycles-of-domestic-violence.jpg'

export default defineComponent({
  name: 'IndexPage',
  components: {
    FormComponent
  },
  setup() {
    const mostrarFormulario = ref(false)

    const backgroundStyle = `min-height: 100vh; background-image: url(${bgImage}); background-size: cover; background-position: center;`

    return {
      mostrarFormulario,
      backgroundStyle
    }
  }
})
</script>

<style scoped>
body {
  margin: 0;
}
</style>
