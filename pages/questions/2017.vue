<template>
  <page>
        <p>Here are all the questions that we came up with in early 2017, on our back from Boston, we stopped in Ipswitch Ohio.</p>
        <question  v-for="question in questions" :question="question.question" />
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
      fetch(process.env.datastore+"api/collections/get/questions?token="+process.env.api)
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