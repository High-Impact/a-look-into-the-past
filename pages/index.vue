<template>
  <page>
      <h1>{{data}}</h1>
      <h2>Something</h2>
  </page>
</template>

<script>

import Page from '../components/Page'

export default {
  components: {
    Page
  },
  data() {
    return {
      api: process.env.api,
      data: 'loading'
    }
  },
  created() {
    this.search();
  },
  methods: {
    search: function () {
      fetch(`${process.env.datastore}api/collections/listCollections`, {
          headers: { 'Cockpit-Token': process.env.api }
      })
        .then(response => response.json())
        .then(json => {
          this.data = json;
      });
    }
  }
}
</script>