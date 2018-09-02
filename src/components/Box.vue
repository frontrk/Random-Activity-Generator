<template>
  <div>
    <h1></h1>
  
    <section v-if="errored">
      <p>We're sorry, we're not able to retrieve this information at the moment,
        please try back later</p>
    </section>

    <section v-else>
    <div class="container">
        <div class="row is-center">
            <div class="col-6">
                <div class="card">
                    <header>
                        <h1 class="is-center">{{msg}}</h1>
                    </header>
                    <div class="content">
                        <h4 class="is-center"><cite>{{info.activity}}</cite></h4>
                        <ul>
                            <ol>Type of activity: {{info.type}}</ol>
                            <ol>Participants: {{info.participants}}</ol>
                            <ol>Accesibility:{{info.accessibility}} <meter value="0.5" min="0" max="1"></meter></ol>
                            <ol>price: {{info.price}}</ol>
                            <ol> {{info.key}}</ol>
                        </ul>
                    </div>
                    <footer class="is-right">
                        <a v-on:click="" class="button primary">Generate again</a>
                    </footer>
                </div>
            </div>
        </div>
    </div>


   </section>   
  </div>
</template>

<script>

import axios from 'axios';

export default {
  name: 'Box',
  props: {
    msg: String
  },
  data() {
    return {
      info: 0,
      errored: false
    }
  },
  mounted () {
    axios
      .get('https://www.boredapi.com/api/activity')
      .then(response => (this.info = response.data))
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

* {
    font-family: "Helvetica", sans-serif;
  }
  .card {
    background: rgba(26, 159, 96, 0.2);
  }
  .row {
    margin: 10rem auto;
  }
  .content {
    padding: 2rem;
  }
  h4 {
    padding: 2rem;
  }
  h1 {
    display: inline;        
    letter-spacing: 5px;
    color: rgb(0, 0, 0);
    text-shadow: 3px 3px rgba(26, 159, 96, 0.2);
  }
  ol {
    padding: 1rem; 
}
</style>
