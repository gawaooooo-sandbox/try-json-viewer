<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="8">
      <v-card class="logo py-4 d-flex justify-center">
        <NuxtLogo />
        <VuetifyLogo />
      </v-card>
      <v-card>
        <v-card-title class="headline">
          Json viewer, Json diff test
        </v-card-title>
        <v-card-text>
          <p>jsonを整形して表示する &amp; jsonを比較して表示するテスト</p>
          <hr class="my-3" />
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="primary" nuxt to="/pretty-print">
            Pretty Print Json
          </v-btn>
          <v-btn color="primary" nuxt to="/vue-json-viewer">
            vue-json-viewer
          </v-btn>
          <v-btn color="primary" nuxt to="/json-diff-patch">
            jsondiffpatch
          </v-btn>
          <v-btn color="primary" nuxt to="/json-diff"> json-diff </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',
}
</script>
