<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
import jwt_decode from "jwt-decode";
import {getUser} from '@/utils/auth'
export default {
  name: "app",
  created() {
    if (getUser().token) {
      const decode = jwt_decode(getUser().token);
      this.$store.dispatch("setIsAutnenticated", !this.isEmpty(decode));
      this.$store.dispatch("setUser", decode);
    }
  },
  methods: {
    isEmpty(value) {
      return (
        value === undefined ||
        value === null ||
        (typeof value === "object" && Object.keys(value).length === 0) ||
        (typeof value === "string" && value.trim().length === 0)
      );
    }
  }
};
</script>

<style>
html,
body,
#app {
  width: 100%;
  height: 100%;
}

</style>
