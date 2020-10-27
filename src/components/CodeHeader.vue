<template>
  <div class="container">
    <h1>{{ code }}</h1>
  </div>
</template>

<script>
import codes from "../assets/mythbusters.json";
let pure_codes = codes.map((entry) => entry.name);

export default {
  name: "CodeHeader",
  data: () => {
    return {
      code: null,
    };
  },
  created() {
    // Generate a random one
    this.code = this.new_code();

    // Bing keystrokes
    window.addEventListener("keydown", (e) => {
      switch (e.keyCode) {
        case 32: // Space
          this.code = this.new_code();
          break;
        case 91: // Command
          this.super_is_down = true;
          break;
        case 67: // C
          if (this.super_is_down) {
            // Trigger copy
            console.log("Trigger Copy");
          }
          break;
        default:
          break;
      }
    });
    window.addEventListener("keyup", (e) => {
      switch (e.keyCode) {
        case 91: // Command
          this.super_is_down = false;
          break;
        default:
          break;
      }
    });
  },
  methods: {
    new_code() {
      let old_code = this.code,
        new_code = this.code;
      while (old_code === new_code) {
        new_code = pure_codes[Math.floor(Math.random() * pure_codes.length)];
      }
      return new_code;
    },
  },
};
</script>

<style scoped>
.container {
  margin-left: auto;
  margin-right: auto;
}
h1 {
  font-size: 8vw;
}
</style>
