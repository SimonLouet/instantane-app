<template>
  <q-page class="flex flex-center">
    <img
      alt="Quasar logo"
      src="~assets/quasar-logo-vertical.svg"
      style="width: 200px; height: 200px"
    >
    <div>
      <button @click="login">Log in</button>
    </div>
    <div>
      <button @click="doSomethingWithToken">token</button>
    </div>
    <pre>
      <code>{{ this.$auth0.user }}</code>
    </pre>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexPage',
  data: function () {
    return {
      user: this.$auth0.user,
    };
  },
  methods: {
      login() {
        this.$auth0.loginWithRedirect();
      },
      async doSomethingWithToken() {
        const token = await this.$auth0.getAccessTokenSilently();
        const response = await fetch('https://xn--instantan-cs-jeb.com/api/authors', {
          headers: {
            Authorization: 'Bearer ' + token
          }
        });
        const data = await response.json();
        console.log(data);
      }
    }
})


</script>
