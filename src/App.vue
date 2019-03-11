<template>
  <div id="app">
    <Sort @sort-by="sortBy"></Sort>
    <div class="main__wrapper">
      <Card :key="item.id" v-for="item in items" :item="item"></Card>
    </div>
  </div>
</template>

<script>
import { data } from "./data.js";
import Card from "./components/Card.vue";
import Sort from "./components/Sort.vue";

export default {
  name: "app",
  data() {
    return {
      items: data,
      user: {
        latitude: 55.7536232,
        longitude: 37.6199775
      }
    };
  },
  components: {
    Card,
    Sort
  },
  methods: {
    sortBy(type) {
      switch (type) {
        case "price":
          this.items.sort((a, b) => {
            return a.price - b.price;
          });
          break;
        case "distance":
          this.items.sort((a, b) => {
            return (
              ((b.dealer.latitude || 0) - this.user.latitude) ** 2 +
              ((b.dealer.longitude || 0) - this.user.longitude) ** 2 -
              ((a.dealer.latitude || 0) - this.user.latitude) ** 2 -
              ((a.dealer.longitude || 0) - this.user.longitude) ** 2
            );
          });
          break;
      }
    }
  },
  beforeMount() {
    this.sortBy("price");
  }
};
</script>

<style>
body {
  margin: 0;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: rgb(243, 243, 243);
}
@media (min-width: 1200px) {
  .main__wrapper {
    display: grid;
    grid-template-columns: repeat(4, 300px);
    grid-gap: 20px;
    justify-content: space-around;
  }
}
</style>
