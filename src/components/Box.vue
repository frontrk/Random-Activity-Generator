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
              
                <div class="card" >
                    <header>
                        
                        <h1 class="is-center">{{msg}}</h1>
                        
                    </header>
                    <transition name="slide-fade" mode="out-in">
                    <div class="content" :key="info.key">
                      
                        <h4 class="is-center" ><cite>{{info.activity}}</cite></h4>
                      
                        <ul>
                            <ol><span>Type of activity: </span>{{info.type}}</ol>
                            <ol><span>Participants: </span>{{info.participants}}</ol>
                            <ol><span>Accesibility: </span><meter v-bind:value="info.accessibility" min="0" max="0.55"></meter></ol>
                            <ol><span>Price: </span><meter v-bind:value="info.price" min="0" max="0.55"></meter></ol>                            
                        </ul>
                         
                    </div>
                    </transition>
                    <footer class="is-right">
                        <a v-on:click="getActivity" class="button primary">Generate again</a>
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
      errored: false,
      loading: true
    }
  },
  methods : {
    getActivity: function () {
      axios
      .get('https://www.boredapi.com/api/activity')
      .then(response => (this.info = response.data))
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
    }
  },
   beforeMount(){
    this.getActivity()
 },

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

  ul {
      list-style: none;
      margin: 0;
      padding: 0;
  }
  ol {
      text-align: left;
      padding: 1rem;
      
  }
  a {
    cursor: pointer;
  }
  span {
    font-weight: bold;
  }
.slide-fade-enter-active {
  transition: all .2s ease-in-out;
}
.slide-fade-leave-active {
  transition: all .2s cubic-bezier(4.0, 5.5, 2.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active for <2.1.8 */ {
  transform: translateX(20px);
  opacity: 0;
}
</style>
