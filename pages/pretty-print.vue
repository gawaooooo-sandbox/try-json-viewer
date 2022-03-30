<template>
  <v-card>
    <v-card-title>pretty-print-json</v-card-title>
    <v-card-text>
      <!-- eslint-disable-next-line vue/no-v-html -->
      <div class="json-container json-wrap" v-html="jsonA"></div>
      <!-- eslint-disable-next-line vue/no-v-html -->
      <div class="json-container json-wrap" v-html="jsonB"></div>
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
import { prettyPrintJson, FormatOptions } from 'pretty-print-json'
import Vue from 'vue'
import exampleJsonA from '~/example/a.json'
import exampleJsonB from '~/example/b.json'

const options: FormatOptions = { quoteKeys: true, indent: 4 }
const prettyPrint = {
  jsonA: prettyPrintJson.toHtml(exampleJsonA, options),
  jsonB: prettyPrintJson.toHtml(exampleJsonB, options),
}

export default Vue.extend({
  data() {
    return {
      jsonA: prettyPrint.jsonA,
      jsonB: prettyPrint.jsonB,
    }
  },
  mounted() {
    console.log(prettyPrint.jsonA)
    console.log(prettyPrint.jsonB)
  },
})
</script>

<style lang="scss">
@import 'pretty-print-json';

.json-wrap {
  display: block;
  white-space: pre;
  margin: 0px;
  overflow: scroll;
}
</style>
