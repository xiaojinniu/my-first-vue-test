<template>
  <div class="hello">
    <h1 v-text="title"></h1>
    <input v-model="newItem" @keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-bind:class="{finished : item.isFinished}" v-on:click="toggleFinish(item)">{{item.label}}</li>
    </ul>
    <p>child tells me: {{ childWords }}</p>
    <component-a msgfromfather="youdie!" v-on:child-tell-me-something="listenToMyBoy"></component-a>
  </div>
</template>

<script>
import Store from '@/util/store.js'
import ComponentA from './componentA'

export default {
  name: 'hello',
  data () {
    return {
      title: 'Welcome to Your Vue.js App',
      items:Store.fetch(),
      newItem: "",
      childWords: ""
    }
  },
  components: { ComponentA },
  methods: {
    toggleFinish: function(item) {
      item.isFinished = !item.isFinished;
    },
    addNew: function() {
      this.items.push({
        label: this.newItem,
        isFinished: false
      });
      this.newItem = "";
    },
    listenToMyBoy: function(msg) {
      console.log(msg);
      this.childWords = msg; 
    }
  },
  watch: {
    items: {
      handler: function(items) {
        Store.save(items);
      },
      deep:true
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.finished{
  text-decoration: underline;
}
h1, h2 {
  font-weight: normal;
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
