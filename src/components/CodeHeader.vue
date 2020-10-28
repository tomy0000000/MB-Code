<template>
  <div class="container">
    <h1 id="code" class="animate__animated animate__faster">{{ code }}</h1>
    <p>From episode {{ episode }} of {{ season }}.</p>
  </div>
</template>

<script>
import "animate.css";
import ClipboardJS from "clipboard";
import codes from "../assets/mythbusters.json";

export default {
  name: "CodeHeader",
  data: () => {
    return {
      code: null,
      episode: null,
      season: null,
    };
  },
  created() {
    // Generate a random code on start
    this.new_code();

    // Bing keystrokes
    window.addEventListener("keydown", (event) => {
      switch (event.key) {
        case " ":
          this.new_code();
          break;
        case "Meta":
        case "Control":
          this.super_is_down = true;
          break;
        case "c":
          if (this.super_is_down) {
            // Copy to clipboard
            var fakeElement = document.createElement("button");
            new ClipboardJS(fakeElement, {
              text: () => this.code,
            });
            fakeElement.click();
            fakeElement.remove();
            // Add animate on header
            const code_element = document.querySelector("#code");
            code_element.classList.add("animate__tada");
            code_element.addEventListener("animationend", () => {
              code_element.classList.remove("animate__tada");
            });
          }
          break;
        default:
          break;
      }
    });
    window.addEventListener("keyup", (event) => {
      switch (event.key) {
        case "Meta":
        case "Control":
          this.super_is_down = false;
          break;
        default:
          break;
      }
    });
  },
  methods: {
    new_code() {
      let new_code;
      do {
        new_code = codes[Math.floor(Math.random() * codes.length)];
      } while (this.code === new_code.name);
      this.code = new_code.name;
      this.episode = new_code.episode;
      this.season = new_code.season;
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
p {
  font-size: 2vw;
}
</style>
