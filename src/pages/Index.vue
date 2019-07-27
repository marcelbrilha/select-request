<template>
  <div>
    <div class="row container-example">
      <div class="col-md-12 col-sm-12 col-xs-12 col-lg-6 col-xl-6 q-pa-sm">
        <h1 class="q-title">Example with filter and radio</h1>
        <q-field>
          <select-request
            label="UF"
            url="https://servicodados.ibge.gov.br/api/v1/localidades/estados"
            :filter="true"
            :radio="true"
            :configOptions="configOptions"
            v-model="uf"
          />

          <p style="margin: 10px 0;"><small>UF selecionada: {{ uf }}</small></p>
        </q-field>
      </div>

      <div class="col-md-12 col-sm-12 col-xs-12 col-lg-6 col-xl-6 q-pa-sm">
        <h1 class="q-title">Example error and retry</h1>
        <q-field>
          <select-request
            label="UF"
            url="https://servicodados.ibge.gov.br/api/v1/localidades/estado"
            :configOptions="configOptions"
            :filter="true"
            :radio="true"
            v-model="uf"
            @error="handleErrorEmitted"
          />
        </q-field>
      </div>
    </div>
  </div>
</template>

<script>
import SelectRequest from '../components/form/SelectRequest'

export default {
  name: 'pageExample',
  components: { SelectRequest },

  created () {
    // Example setDefault value 11
    this.uf = 11
  },

  data () {
    return {
      uf: '',
      configOptions: {
        label: 'sigla',
        value: 'id'
      }
    }
  },

  methods: {
    handleErrorEmitted () {
      console.log('Handle error emitted')
    }
  }
}
</script>

<style lang="css" scoped>
  .container-example {
    padding: 20px;
  }
</style>
