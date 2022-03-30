<template>
  <v-card>
    <v-card-title>vue-json-viewer</v-card-title>
    <v-card-text>
      <v-card-subtitle>default</v-card-subtitle>
      <VueJsonViewer :value="jsonA"></VueJsonViewer>

      <v-card-subtitle>show-double-quotes</v-card-subtitle>
      <VueJsonViewer :value="jsonA" show-double-quotes></VueJsonViewer>

      <v-card-subtitle>copyable boxed</v-card-subtitle>
      <VueJsonViewer :value="jsonB" copyable boxed></VueJsonViewer>

      <v-card-subtitle>expanded expand-depth=2</v-card-subtitle>
      <VueJsonViewer :value="jsonB" expanded :expand-depth="2"></VueJsonViewer>

      <v-card-subtitle>preview-mode</v-card-subtitle>
      <VueJsonViewer :value="jsonB" preview-mode></VueJsonViewer>

      <v-card-subtitle>
        expanded expand-depth=2 show-array-index=false
      </v-card-subtitle>
      <VueJsonViewer
        :value="jsonB"
        expanded
        :expand-depth="2"
        :show-array-index="false"
      ></VueJsonViewer>
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue'
import VueJsonViewer from 'vue-json-viewer'
import 'vue-json-viewer/style.css'
import exampleJsonA from '~/example/a.json'
import exampleJsonB from '~/example/b.json'

export default Vue.extend({
  components: { VueJsonViewer },
  data() {
    return {
      jsonA: exampleJsonA,
      jsonB: exampleJsonB,
    }
  },
})
</script>
