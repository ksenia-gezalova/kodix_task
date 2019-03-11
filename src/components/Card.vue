<template>
  <div class="card">
    <img class="card__img" :src="item.images[0]" alt="name">
    <h2 class="card__title">{{ item.name }}</h2>
    <p class="card__price">{{ item.price }}₽</p>
    <ul class="card__list">
      <li
        class="card__item"
        v-for="(feature,index) in item.features.slice(0,sublist ? item.features.length : 3)"
        :key="index"
      >{{ feature }}</li>
      <li
        v-if="item.features.length > 3"
        class="card__link"
        @click="sublist=true"
        v-show="!sublist"
      >еще {{ item.features.length-3 }} {{ suffixator('особенност', item.features.length - 3) }}</li>
      <li class="card__link" @click="sublist=false" v-show="sublist">Свернуть...</li>
    </ul>
    <a class="card__address" :href="item.dealer.url">
      <img src="../assets/pin.svg" class="card__icon">
      {{ item.dealer.name }}, {{ item.dealer.city }}, {{ item.dealer.address}}
    </a>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["item"],
  data() {
    return {
      sublist: false
    };
  },
  methods: {
    suffixator(word, amount) {
      if (amount % 10 === 1 && amount % 100 != 11) return word + "ь";
      else if (
        amount % 10 > 1 &&
        amount % 10 < 5 &&
        Math.floor((amount % 100) / 10) !== 1
      )
        return word + "и";
      else return word + "ей";
    }
  }
};
</script>

<style lang="scss" scoped>
.card {
  background-color: #fff;
  padding: 20px;
  padding-bottom: 0;
  margin: 0 auto;
  margin-bottom: 20px;
  max-width: 320px;

  @media (min-width: 1200px) {
    margin: 0;
  }

  &__img {
    width: 200px;
  }
  &__price {
    font-weight: 700;
  }
  &__title {
    margin: 0;
    color: rgb(79, 182, 216);
  }
  &__link {
    list-style: none;
    color: rgb(79, 182, 216);
    margin-left: -16px;
    cursor: pointer;
    transition: all 0.3s;

    &:hover {
      color: rgb(31, 135, 170);
    }
  }
  &__address {
    border-top: 1px solid #eeeeee;
    margin: 0 -20px;
    display: flex;
    align-items: center;
    color: rgb(79, 182, 216);
    text-decoration: none;
    transition: all 0.3s;
    padding: 15px;

    &:hover {
      color: rgb(31, 135, 170);
    }
  }
  &__icon {
    width: 40px;
    height: 40px;
    margin-right: 10px;
    flex-shrink: 0;
  }
}
</style>

