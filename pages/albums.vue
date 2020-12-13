<template>
  <page>
      <div class="sortAndFilter"  v-bind:class="{ 'isShowing' : sortAndFilterShowing }">
        <h2 @click="togglesortAndFilter" class="font-bold text-gray-700 flex justify-between items-center w-full">Sort & Filter Options <fa class="chev" icon="chevron-down" /></h2>
        <div class="flex justify-end py-4 text-gray-500 toolBox">
          <select 
            name="year" 
            id="year-select" 
            @change="filterYear"
            class="rounded border shadow-sm p-2 w-1/2 mr-auto bg-white"
          >
              <option value="all">Filter by Year</option>
              <option v-for="year in yearOptions" :key="year" :value="year">{{year}}</option>
          </select>

          <button class="rounded border shadow-sm p-2 mr-2" @click="toggleFilterOptionsShowing"><fa icon="filter"  /></button>
          <button class="rounded border shadow-sm p-2 " @click="sortByDate" ><fa v-if="oldestFirst" icon="sort-amount-up-alt"  /><fa v-else icon="sort-amount-down-alt"  /></button>
        </div>
        <div v-bind:class="{ 'foIsShowing' : filterOptionsShowing }"  class="filterOptions fixed h-full w-full top-0 left-0">
          <div class="container mx-auto px-12 py-12 pt-8">
            <div class="filterOptionsContainer bg-white border rounded shadow p-4">
              <div class="filterHeader flex justify-between items-center text-gray-700 text-2xl font-bold b">
                <h2 class="">Filter Options</h2>
                <fa @click="toggleFilterOptionsShowing" class="" icon="times"/>
              </div>
              <!-- <hr class="my-4"> -->
              <div class="mt-4">
                <h3 class="text-gray-700 font-bold">Album Types</h3>
                <div class="flex flex-wrap mt-2">
                  <button 
                    @click="filterByType('all')"
                    class="border rounded p-2 text-xs mr-2 uppercase font-bold text-gray-500"
                  >
                    All
                  </button>
                  <button 
                    v-for="type in typeOptions" 
                    :key="type"
                    @click="filterByType(type)"
                    class="border rounded p-2 text-xs mr-2 uppercase font-bold text-gray-500"
                  >
                    {{type}}
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
        <hr class="my-2">
      </div>
      <template v-if="filtered">
          <div v-if="filteredList.length == 0" class="p-4 mt-4 border rounded shadow-sm">
            <h2 class="font-bold text-red-500 text-2xl">Ya dumb fuck</h2>
            <p class="">There's nothing here, try again, or don't. I don't care.</p>
          </div>

          <album 
            v-for="album in filteredList"
            :key="album._id" 
            :img="datastore + album.img.path" 
            :link="album.link" 
            :header="album.header" 
            :desc="album.description" 
            :type="album.type" 
            :weight="parseInt(album.weight)" 
            :date="album.date" 
          />
      </template>
      <template v-else>
        <album
          v-for="album in albums"
          :key="album._id" 
          :img="datastore + album.img.path" 
          :link="album.link" 
          :header="album.header" 
          :desc="album.description" 
          :type="album.type" 
          :weight="parseInt(album.weight)" 
          :date="album.date" 
        />
      </template>
  </page>
</template>

<script>

import Page from '../components/Page'
import Album from '../components/Album'

export default {
  components: {
    Page,
    Album
  },
  data() {
    return {
      albums:Array,
      datastore: process.env.datastore,

      sortAndFilterShowing:false,
      filterOptionsShowing:false,
      
      yearOptions:Array,
      typeOptions:Array,
      
      oldestFirst:true,
      
      filtered: false,
      filteredList:Array,
      filteredByType:Array,


    }
  },
  methods: {
    
    filterYear: function(e) {
      const selectedOption = e.target.value;

      if(selectedOption == "all") {
        this.filtered = false;
        this.filteredList = [];
      } else {
        this.filtered = true;
        this.filteredList = this.albums.filter(album => album.date.slice(0,4) == selectedOption);
      }
    },

    filterByType: function(type) {

      if(type == "all") {
        this.filtered = false;
        this.filteredList =  this.albums;
      } else {
        this.filtered = true;
        this.filteredList = this.albums.filter(album => album.type == type);
      }
    },

    filterButtons: function(type) {
      console.log('hello '+type);
    },

    compare: function(a, b) {
          if (a.date < b.date)
            console.log('test')
            return -1;
          if (a.date > b.date)
            console.log('testing')
            return 1;
          console.log('testinging')
          return 0;
    },

    sortByDate: function() {
      if (this.filteredList) {
        if (this.filteredList.length > 1) {
          this.albums = this.albums.sort(this.compare);
          this.filteredList = this.filteredList.sort(this.compare);
          this.oldestFirst = !this.oldestFirst;
        } else {
          this.albums = this.albums.sort(this.compare);
          this.oldestFirst = !this.oldestFirst;
        }
      } else {
        this.albums = this.albums.sort(this.compare);
        this.oldestFirst = !this.oldestFirst;
      }
    },

    togglesortAndFilter: function() {
      this.sortAndFilterShowing = !this.sortAndFilterShowing;
    },

    toggleFilterOptionsShowing: function() {
      this.filterOptionsShowing = !this.filterOptionsShowing;
    }
  },
  created() {
      fetch(process.env.datastore+"api/collections/get/albums?sort[date]=-1&token="+process.env.api)
        .then(response => { 
            if(response.ok){
                return response.json()    
            } else{
                console.log("Server returned " + response.status + " : " + response.statusText);
            }                
        })
        .then(response => {
            console.log(response);
            this.albums = response.entries
            let allYears = this.albums.map(album => album.date.slice(0,4));
            let allTypes = this.albums.map(album => album.type);
            function onlyUnique(value, index, self) {
              return self.indexOf(value) === index;
            }
            this.yearOptions = allYears.filter(onlyUnique)
            this.typeOptions = allTypes.filter(onlyUnique)
            console.log(this.typeOptions);
        })
        .catch(err => {
            console.log(err);
        });
  }
}
</script>

<style scoped>
/* All the time */
.sortAndFilter * {
  transition:375ms ease;
}
.sortAndFilter h2 {
  opacity:.7;
}
.sortAndFilter .toolBox {
  padding:0;
  max-height:1px;
  opacity: 0;
  visibility: hidden;
}

/* Is showing TRUE */
.isShowing h2 {
  opacity:1;
}
.isShowing .chev{
  transform: rotateX(180deg);
}
.isShowing .toolBox {
  padding:1rem 0;
  max-height:100vh;
  opacity: 1;
  visibility: visible;
}

/* Styles for the filter modal */

.filterOptions {
  z-index:99999;
  transition:375ms ease;
  visibility: hidden;
}
.filterOptions.foIsShowing {
  background:rgba(255,255,255,.95);
  visibility: visible;
}
.filterOptionsContainer {
  opacity: 0;
  transform:scale(.25) translateY(50vh);
}
.foIsShowing .filterOptionsContainer {
  opacity:1;
  transform:scale(1) translateX(0);
}
</style>