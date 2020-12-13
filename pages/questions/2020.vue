<template>
  <page>
        <p>These are the questions that we came up with in early 2020 right around the time COVID-19 starting taking on full effect.</p>
        <question  v-for="question in questions" :question="question.question" :key="question._id" />
  </page>
</template>

<script>

import Page from '../../components/Page'
import Question from '../../components/Question'

export default {
  components: {
    Page,
    Question
  },
  data() {
      return {
          questions: Array
      }
  },
  created() {
      fetch(process.env.datastore+"api/collections/get/questions?filter[group]=5fca3524313330c3bc00024a&token="+process.env.api)
        .then(response => { 
            if(response.ok){
                return response.json()    
            } else{
                console.log("Server returned " + response.status + " : " + response.statusText);
            }                
        })
        .then(response => {
            console.log(response);
            this.questions = response.entries
        })
        .catch(err => {
            console.log(err);
        });
  },
  methods: {
  }
}
</script>