<template>
  <div>
    isDisabled: {{isDisabled}} <br/>
    OnClick Change: {{time || '...'}} <br/>
    <button :disabled="isDisabled" @click="doSomething"> A Button </button>
    <button @click="doSomething"> A Button Always Enabled </button>
  </div>

</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      isDisabled: false,
      time: 0,
    }
  },
  methods: {
    toggle() {
      this.isDisabled = !this.isDisabled;
    },
    doSomething() {
      this.toggle();
      console.log('did something')
      this.time = Date.now();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
