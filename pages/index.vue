<template>
  <page>
      <div class="">
        <div class="">
          <h2 class="font-bold text-2xl mb-2">Howdy! Y'all</h2>
          <p class="text-lg ">This is <em>a look into the a past</em>. The goal is provide a digital archive of our lives. The site is currently broken up into 2 sections.</p>
          <hr class=" mt-4">
        </div>
        <card />
        <card />
      </div>
  </page>
</template>

<script>

import Page from '../components/Page'
import Card from '../components/Card'

export default {
  components: {
    Page,
    Card
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