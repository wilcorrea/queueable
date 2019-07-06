<template>
  <div>
    <pre>AppPai</pre>
    <pre>{{ record }}</pre>
    <button @click="queue">Click me</button>
    <hr>
    <AppFilho v-model="record.addresses"/>
  </div>
</template>

<script>
import AppFilho from "./AppFilho";
import Queueable from "./Queueable";
export default {
  name: "AppPai",
  components: {
    AppFilho
  },
  data: () => ({
    record: {
      name: "William",
      addresses: [
        {
          where: "Somewhere"
        }
      ]
    }
  }),
  methods: {
    queue() {
      const options = {
        onStart: (queue, payload) => {
          console.log("~> onStart: ", JSON.parse(JSON.stringify(queue)));
        },
        onWalk: (current, payload) => {
          console.log("~> onWalk: ", current, payload);
        },
        onProgress: (current, payload) => {
          console.log("~> onProgress: ", current, payload);
        },
        onEnd: (payload) => {
          const { counter } = payload
          console.log("~> onEnd: ", payload);
          if (counter >= 10) {
            return;
           }
          if (window.confirm('Faz mais?')) {
            return ["f", "g", "h", "i", "j"];
           }
        },
        onFinish: (payload) => {
          console.log("~> onFinish: ", payload);
        }
      };
      Queueable.build(options).run(["a", "b", "c", "d", "e"]);
    }
  }
};
</script>

