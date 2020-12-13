<template>
  <page>
      <div class="">
      
        <div class="">
          <h2 class="font-bold text-2xl mb-2">Hey!</h2>
          <p class="text-lg ">You've found <em>a look into the a past</em>. This is the one stop shop for our digital archive. The site is currently broken up into 2 sections.</p>
        </div>
        
        <card img="https://alip.cp.highimpact.design/storage/uploads/2020/12/07/5fcea751ba422On-the-water-2.jfif" title="Albums" desc="A collection of all our photos and videos" link="/albums" />
        <card img="https://alip.cp.highimpact.design/storage/uploads/2020/12/05/5fcbfb4c145aequestions-sm.jpg" title="Questions" desc="A collection of all the questions" link="/questions" />
      
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
      datastor: process.env.datastore,
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