<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button v-on:click="getJokes">Get jokes</button>
    <ul>
      <li v-for="item in jokes" :key="item.id">
        {{ item.joke }}
      </li>
    </ul>
  </div>
</template>
<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',
  data() {
    return {
      jokes: [],
      loading: false,
      msg: null,
    };
  },
  methods: {
    getJokes() {
      this.loading = true;
      axios.get('http://api.icndb.com/jokes')
        .then((response) => {
          this.loading = false;
          this.jokes = response.data.value;
        }, () => {
          this.loading = false;
        });
    },
  },
};

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  h3 {
    margin: 40px 0 0;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
</style>
