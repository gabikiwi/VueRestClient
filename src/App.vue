<template>
  <div id="app">
    <header>
      <span>Testing API App</span>
    </header>
    <main>
        <h2>Test URL</h2>
        <div>
           <input v-model="testUrl"/>
           <button id="btn" class="" v-on:click="getInternalResults">Get Internal Results</button>
        </div>
       
        
        <button id="btn" class="" v-on:click="getOnlineResults">Get Online Results</button>
        
        <div v-if="loading">
          <img src="../src/assets/tenor.gif"/>
          Loading.....
        </div>

        <div class="row">
          <div class="col-md-4 cards">
            <div>
              <h3>{{ internalResults }}</h3>
            </div>
          </div>
        </div>

     <div class="wrapper">
      <div class="row">
          <div v-for="result in onlineResults" :key="result.id">
          <div class="col-md-4 cards">
            <div>
              <h3>{{ result.id }}</h3>
              <p>{{ result.joke }}</p>
              <p>{{ result.category }}</p>
            </div>
          </div>
          </div>
        </div> 

        


      </div>
    </main>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "app",
  data() {
    return {
      testUrl : "https://reqres.in/api/users/2",
      onlineResults: [],
      internalResults: [],
      loading: false
    };
  },
  methods: {


    getInternalResults: function() {
      this.loading = true;
     axios.get(this.testUrl).then(
        response => {
          this.loading = false;
          this.internalResults = response.data;
        },
        error => {
          this.loading = false;
        }
      );
    },

    getOnlineResults: function() {
      this.loading = true;
      axios.get("http://api.icndb.com/jokes/random/1").then(
        response => {
          this.loading = false;
          this.onlineResults = response.data.value;
        },
        error => {
          this.loading = false;
        }
      );
    }

 
  }
};
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

main {
  text-align: center;
  margin-top: 40px;
}

header {
  margin: 0;
  height: 56px;
  padding: 0 16px 0 24px;
  background-color: #35495e;
  color: #ffffff;
}

header span {
  display: block;
  position: relative;
  font-size: 20px;
  line-height: 1;
  letter-spacing: 0.02em;
  font-weight: 400;
  box-sizing: border-box;
  padding-top: 16px;
}

button {
  background: #51b767;
  color: #ffffff;
  padding: 15px;
  border-radius: 0;
  font-weight: bold;
  font-size: 15px;
  border: 0;
}

.cards {
  background: #f5f5f5;
  height: 400px;
}
.cards:hover {
  transform: translateY(-0.5em);
  background: #ebebeb;
}

.cards {
  column-count: 1;
  column-gap: 1em;
  margin-top: 70px;
}
</style>
