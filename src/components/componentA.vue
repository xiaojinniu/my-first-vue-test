<template>
  <div class="hello">
    <h1>{{msg}}</h1>
    <button v-on:click="onClickMe">Click!</button>
  </div>
</template>

<script>
import Store from '@/util/store.js'

export default {
  data () {
    return {
      msg: 'Welcome to Your componentA'
    }
  },
  props: ["msgfromfather"],
  methods: {
    onClickMe: function() {
      console.log(this.msgfromfather);
      this.$emit('child-tell-me-something', this.msg);
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
