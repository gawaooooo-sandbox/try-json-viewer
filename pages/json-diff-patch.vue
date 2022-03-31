<template>
  <v-card>
    <v-card-title>jsondiffpatch</v-card-title>
    <v-card-text>
      <a href="https://benjamine.github.io/jsondiffpatch/demo/index.html">
        jsondiffpatch demo page
      </a>
      <v-card-subtitle>visual diff</v-card-subtitle>
      <div class="ma-1">
        <v-btn color="primary" @click="runScriptTags($refs.visualDiff)">
          runScriptTag
        </v-btn>
        <v-btn color="secondary" @click="toggleShowUnchanged()">
          toggleShowUnchanged
        </v-btn>
      </div>

      <div ref="visualDiff" class="json-container" v-html="diffs"></div>
      <v-divider></v-divider>
      <v-card-subtitle>annotated</v-card-subtitle>
      <div class="json-container" v-html="annotated"></div>
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
// import * as JSONDiffPatch from 'jsondiffpatch'
import { create, formatters } from 'jsondiffpatch'
import Vue from 'vue'
import leftJson from '~/example/left.json'
import rightJson from '~/example/right.json'

import 'jsondiffpatch/dist/formatters-styles/html.css'
import 'jsondiffpatch/dist/formatters-styles/annotated.css'
// console.log(JSONDiffPatch)

// @see http://shokai.org/blog/archives/10643
// @see https://github.com/benjamine/jsondiffpatch/blob/master/docs/arrays.md
const jsondiffpatch = create({
  objectHash: (obj: any, index: number) => {
    // try to find an id property, otherwise just use the index in the array
    return obj.name || obj.id || obj._id || '$$index:' + index
  },
})

export default Vue.extend({
  data() {
    return {
      diffs: undefined as any,
      annotated: undefined as any,
      showUnchanged: false,
    }
  },
  mounted() {
    const delta = jsondiffpatch.diff(leftJson, rightJson)
    console.log(delta)
    if (delta) {
      this.diffs = formatters.html.format(delta, leftJson)
      this.annotated = formatters.annotated.format(delta, leftJson)
      formatters.html.hideUnchanged()

      this.$nextTick(() => {
        this.runScriptTags(this.$refs.visualDiff)
      })
    }
  },
  methods: {
    toggleShowUnchanged() {
      console.log('--- call toggleShowUnchanged')
      this.showUnchanged = !this.showUnchanged
      if (this.showUnchanged) {
        formatters.html.showUnchanged(true)
      } else {
        formatters.html.hideUnchanged()
      }
      // this.runScriptTags(this.$refs.visualDiff)
      this.$nextTick(() => {
        this.runScriptTags(this.$refs.visualDiff)
      })
    },
    // @see https://github.com/benjamine/jsondiffpatch/blob/master/docs/demo/demo.js#L252
    runScriptTags(el: Vue | Element | (Vue | Element)[] | undefined) {
      console.log('--- call runScriptTags')
      if (!el) {
        return
      }
      const scripts = (el as Element).querySelectorAll('script')
      console.log(scripts)
      for (let i = 0; i < scripts.length; i++) {
        const s = scripts[i]
        // eslint-disable-next-line no-eval
        eval(s.innerHTML)
      }
    },
  },
})
</script>

<style lang="scss">
.json-container {
  background-color: white;
  color: black;
  /* display: block;
  white-space: pre;
  margin: 0px; */
  overflow: auto;
}
</style>
