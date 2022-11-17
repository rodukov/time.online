<template>
  <div class="home">

    {{ request_data }}
    <!--div class="repository" v-for="item in request_data" :key="item">
      {{ item }}
    </div-->


  </div>
</template>


<script>
import axios from 'axios'


export default {
  name: 'Home',
  data() { 
    return {
      request_data: []
    }
  },
  mounted() {
    this.time()
  },
  methods: {
    async time() {
      await axios
        .get('https://worldtimeapi.org/api/timezone/Europe/London')
        .then(response => (this.request_data = response["data"]))
        // .catch(function (error) { this.error_axios = error.status })
    }
  }
}
</script>