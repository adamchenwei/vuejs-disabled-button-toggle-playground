<template>
  <div>
    isDisabled: {{isDisabled}} <br/>
    OnClick Change: {{time || '...'}} <br/>
    <button :disabled="isDisabled" @click="doSomething"> A Button </button>
    <button @click="doSomething"> A Button Always Enabled </button>

    <h1>a recaptcha enabled button can't add disabled attribute!!!</h1>
    <vue-recaptcha
      ref="recaptcha"
      @verify="onVerify"
      @expired="onExpired"
      sitekey="6Lfe33gUAAAAAMCuDwRfhSUV4sGkqGDaGrKqjkmZ">
      <button @click="doSomething"> A Button With Recaptcha </button>
    </vue-recaptcha>
  </div>

</template>

<script>
import VueRecaptcha from 'vue-recaptcha';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  components: {
    VueRecaptcha,
  },
  data() {
    return {
      isDisabled: false,
      time: 0,
    }
  },
  methods: {
    resetCaptcha() {
      //strange thing need this timeout to get around recaptcha style error
      console.log('recaptcha reset!!')
      setTimeout(() => grecaptcha.reset(), 1000)
    },
    onVerify() {
      console.log('did onVerify')
      this.resetCaptcha()
    },
    onExpired() {
      console.log('did onExpired')
      this.resetCaptcha()
    },
    toggle() {
      this.isDisabled = !this.isDisabled;
    },
    doSomething() {
      this.toggle();
      console.log('did something')
      this.time = Date.now();
      // this.resetCaptcha()
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
