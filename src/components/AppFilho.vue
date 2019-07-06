<template>
  <div>
    <pre>AppFilho</pre>
    <pre>{{ addressess }}</pre>
    <hr>
    <template v-for="(address, key) in addressess">
      <AppNeto :key="key" :value="address.where" @input="input(key, 'where', $event)"/>
    </template>
  </div>
</template>

<script>
import AppNeto from "./AppNeto";
export default {
  name: "AppFilho",
  components: {
    AppNeto
  },
  props: ["value"],
  data: () => ({
    addressess: []
  }),
  methods: {
    input(index, property, value) {
      const address = this.addressess[index];
      address[property] = value;
      const addresses = this.addressess.splice(index, 1, address);
      this.$emit("input", addresses);
    }
  },
  watch: {
    value: {
      immediate: true,
      deep: true,
      handler(addressess) {
        this.addressess = addressess;
      }
    }
  }
};
</script>

