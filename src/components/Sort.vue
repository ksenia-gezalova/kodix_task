<template>
  <div class="sort" @click="update()">
    <p class="sort__title">Сортировать</p>
    <p-radio
      class="p-default p-round"
      name="radio1"
      v-model="isChecked"
      v-bind:value="byPrice"
    >По цене</p-radio>
    <p-radio name="radio1" v-model="isChecked" v-bind:value="byDistance">По удаленности</p-radio>
  </div>
</template>

<script>
export default {
  name: "Sort",
  data() {
    return {
      byPrice: true,
      byDistance: false,
      isChecked: true
    };
  },
  methods: {
    update() {
      setTimeout(() => {
        this.$emit(
          "sort-by",
          this.isChecked === this.byDistance ? "distance" : "price"
        );
      }, 100);
    }
  }
};
</script>


<style lang="scss" scoped>
@import "~pretty-checkbox/src/pretty-checkbox.scss";

.sort {
  display: flex;
  align-items: center;
  padding: 10px;

  &__title {
    margin-right: 10px;
  }
}
</style>

