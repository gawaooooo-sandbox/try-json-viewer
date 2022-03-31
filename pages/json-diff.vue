<template>
  <v-card>
    <v-card-title>json-diff</v-card-title>
    <v-card-subtitle>show console</v-card-subtitle>
    <v-card-text>
      {{ diffs }}
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
import { diffString, diff } from 'json-diff'

import Vue from 'vue'
import exampleJsonA from '~/example/a.json'
import exampleJsonB from '~/example/b.json'

export default Vue.extend({
  data() {
    return {
      diffs: '',
    }
  },
  mounted() {
    this.diffs = diffString(exampleJsonA, exampleJsonB)
    // console.log(diffString(exampleJsonA, exampleJsonB))
    console.log(this.diffs)
    console.log(diff(exampleJsonA, exampleJsonB))
  },
})
</script>
