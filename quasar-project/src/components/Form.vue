<template>
  <q-page class="flex flex-center q-pa-md">
    <div  style="min-width: 300px;">
      <q-form
        @submit.prevent="enviarDenuncia"
        class="bg-white q-pa-md rounded-borders q-gutter-md shadow-2"
      >
        <q-select
          v-model="tipoViolencia"
          label="Tipo de violência"
          :options="['Física', 'Psicológica', 'Sexual', 'Patrimonial', 'Moral']"
          outlined
          dense
        />

        <q-input
          v-model="descricao"
          type="textarea"
          label="Descreva o que aconteceu (opcional)"
          outlined
          dense
        />

        <q-input
          v-model="cep"
          label="CEP"
          outlined
          dense
          mask="#####-###"
          @blur="buscarCep"
        />

        <q-input v-model="logradouro" label="Logradouro" outlined dense />
        <q-input v-model="numero" label="Número" outlined dense />
        <q-input v-model="complemento" label="Complemento (opcional)" outlined dense />
        <q-input v-model="bairro" label="Bairro" outlined dense />
        <q-input v-model="cidade" label="Cidade" outlined dense />
        <q-input v-model="uf" label="Estado (UF)" outlined dense maxlength="2" />

        <q-btn label="Enviar denúncia anônima" type="submit" color="primary" />
      </q-form>
    </div>
  </q-page>
</template>

<script lang="ts">
export default {
  name: 'FormComponent',
  data() {
    return {
      tipoViolencia: '',
      descricao: '',
      cep: '',
      logradouro: '',
      numero: '',
      complemento: '',
      bairro: '',
      cidade: '',
      uf: ''
    }
  },
  methods: {
    async buscarCep() {
      const cepLimpo = this.cep.replace(/\D/g, '')
      if (cepLimpo.length !== 8) {
        this.$q.notify({ type: 'warning', message: 'CEP inválido' })
        return
      }

      try {
        const response = await fetch(`https://viacep.com.br/ws/${cepLimpo}/json/`)
        const data = await response.json()

        if (data.erro) {
          this.$q.notify({ type: 'negative', message: 'CEP não encontrado' })
        } else {
          this.logradouro = data.logradouro
          this.bairro = data.bairro
          this.cidade = data.localidade
          this.uf = data.uf
        }
      } catch (err: unknown) {
        this.$q.notify({ type: 'negative', message: 'Erro ao buscar o CEP' })

        if (err instanceof Error) {
          console.error('Erro de CEP:', err.message)
        }
      }
    },

    enviarDenuncia() {
      console.log('Formulário enviado:', {
        tipoViolencia: this.tipoViolencia,
        descricao: this.descricao,
        cep: this.cep,
        logradouro: this.logradouro,
        numero: this.numero,
        complemento: this.complemento,
        bairro: this.bairro,
        cidade: this.cidade,
        uf: this.uf
      })

      this.tipoViolencia = ''
      this.descricao = ''
      this.cep = ''
      this.logradouro = ''
      this.numero = ''
      this.complemento = ''
      this.bairro = ''
      this.cidade = ''
      this.uf = ''
    }
  }
}
</script>
