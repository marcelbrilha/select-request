<template>
  <div class="container-select-request">
    <q-select
      @input="updateValue"
      :float-label="label"
      :options="options"
      :filter="filter"
      :radio="radio"
      :toggle="toggle"
      :separator="separator"
      :error="error"
      v-model="valueSelect"
    />

    <q-spinner-tail
      size="20px"
      class="spinner-select-request"
      v-if="loading"
    />

    <q-icon
      size="20px"
      class="icon-error-select-request"
      name="error"
      v-if="errorIcon"
      @click.native="request"
    >
      <q-tooltip class="tooltip-select-request">
        Tentar novamente
      </q-tooltip>
    </q-icon>
  </div> <!-- CONTAINER SELECT REQUEST -->
</template>

<script>
import axios from 'axios'

export default {
  name: 'SelectRequest',

  data () {
    return {
      valueSelect: this.value,
      options: [],
      loading: false,
      errorIcon: false
    }
  },

  props: {
    label: String,
    url: String,
    configOptions: Object,
    value: {
      required: false,
      default: ''
    },
    error: Boolean,
    params: Object,
    filter: Boolean,
    radio: Boolean,
    toggle: Boolean,
    separator: Boolean
  },

  watch: {
    url () {
      this.request()
    },

    params () {
      this.request()
    }
  },

  created () {
    this.request()
  },

  methods: {
    /**
     * Reset data
     * @return {[void]}
     */
    reset () {
      this.options = []
      this.loading = false
      this.errorIcon = false
    },

    /**
     * Map the request data to the select format
     * @param  {[Array] Response of request}
     * @return {[void]}
     */
    setOptions (data) {
      const { label, value } = this.configOptions

      this.options = data
        .sort((a, b) => String(a[label]).localeCompare(String(b[label])))
        .map(options => {
          return {
            label: options[label],
            value: options[value]
          }
        })
    },

    /**
     * Make the request to fill in the options
     * @return {[void]}
     */
    request () {
      const params = this.params

      this.reset()
      this.loading = true

      axios.get(this.url, { params })
        .then(response => {
          const data = response.data
          this.loading = false

          if (data && Array.isArray(data)) {
            this.setOptions(data)
          } else {
            this.errorIcon = true
            this.$emit('error', Error('Invalid response data'))
          }
        })
        .catch(error => {
          console.log(`Error in select request: ${error}`)
          this.loading = false
          this.errorIcon = true
          this.$emit('error', error)
        })
    },

    updateValue () {
      this.$emit('input', this.valueSelect)
    }
  }
}
</script>

<style lang="css" scoped>
  .container-select-request {
    position: relative;
  }
  .container-select-request,
  .container-select-request .q-select {
    width: 100%;
  }
  .spinner-select-request,
  .icon-error-select-request {
    position: absolute;
    right: 30px;
    margin-top: -27px;
  }
  .icon-error-select-request {
    cursor: pointer;
  }
  .tooltip-select-request {
    text-align: center;
  }
</style>
