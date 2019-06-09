<template>
  <div id="app" class="center-column">
    <hr />
    <accordion>
      <accordion-item v-for="(item, index) in data" :key="index">
        <template v-slot:header>
          <h4>{{ item.title }}</h4>
        </template>
        <p>
          {{ item.description }}
        </p>
      </accordion-item>
    </accordion>
  </div>
</template>

<script>
import Accordion from "./components/Accordion.vue";
import AccordionItem from "./components/AccordionItem.vue";
import data from "./data/data.json";

export default {
  name: "app",
  data: function() {
    return {
      data: data
    };
  },

  components: {
    Accordion,
    AccordionItem
  }
};
</script>

<style lang="scss">
html {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  box-sizing: border-box;
  position: relative;
  background-color: #efefef;
  padding: 0;
  margin: 0;
}
body {
  padding: 0;
  margin: 0;
}
hr {
  border: none;
}
*,
*:before,
*:after {
  box-sizing: inherit;
}
h1,
h2,
h3,
h4,
h5 {
  margin: 5px 0 5px 0;
  font-family: "Arial Black", Gadget, sans-serif;
}
p {
  margin: 10px 0 10px 0;
}
.center-column {
  position: relative;
  max-width: 1320px;
  margin: 0 auto;
  padding: 0 20px;
}
</style>
