<template>
  <q-layout view="lHh Lpr lFf">
    <!-- Cabeçalho com mensagem de emergência -->
    <q-header elevated class="bg-negative text-white">
      <q-toolbar class="q-px-md">

        <q-icon name="warning" size="md" class="q-mr-sm" />

        <q-toolbar-title class="text-weight-bold">
          Caso esteja em perigo imediato, ligue <span class="text-bold">190</span>
        </q-toolbar-title>

      </q-toolbar>
    </q-header>

    <!-- Conteúdo das páginas -->
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'MainLayout'
})
</script>
