<script setup>
import { ref } from "vue";
import { useRoute, useRouter } from "vue-router";
import { useCart, useFavorites } from "@/composables";
import { useCatalogCategory } from "@/composables/useCatalogCategory";
import VContainer from "@/components/VContainer.vue";
import VRow from "@/components/UI/VRow.vue";
import VCol from "@/components/UI/VCol.vue";
import VButton from "@/components/UI/VButton.vue";
import VCollapse from "@/components/UI/VCollapse.vue";
import VCatalogCard from "@/components/VCatalogCard.vue";
import VLayoutDefault from "@/components/Layouts/VLayoutDefault.vue";
import VHeaderCard from "@/components/VHeaderCard.vue";
import VCustomLayout from "@/components/UI/VCustomLayout.vue";

const route = useRoute();
const router = useRouter();

const filter = ref({
  brand: route.query.brand,
  color: route.query.color,
});

const { products, pagination, getProductsCategory } = useCatalogCategory();
const { onAddToCart } = useCart();
const { onToggleFavorites } = useFavorites();

getProductsCategory(route.params.category, filter.value);

async function onFilter() {
  await getProductsCategory(route.params.category, filter.value);

  router.push({
    query: filter.value,
  });
}

async function onReset() {
  filter.value = {
    brand: undefined,
    color: undefined,
  };

  await getProductsCategory(route.params.category, filter.value);

  router.push({
    query: filter.value,
  });
}

async function onChangePage(page) {
  await getProductsCategory(route.params.category, {
    _page: page,
  });
}

function backPage() {
  router.back();
}
</script>

<template>
  <VLayoutDefault>
    <VContainer class="main">
      <v-row class="custom-container">
        <v-col class="left">
          <v-row>
            <button class="back-button" :onclick="backPage">
              <img src="@/assets/icons/back.svg" alt="" />
            </button>
          </v-row>
          <v-row class="image-container" justify="center">
            <img src="@/assets/images/tarelkabig1.svg" alt="" />
          </v-row>
          <v-row class="card-dilivery-info" justify="beetwen">
            <span class="card-dilivery-text">
              Доставка по всей территории РФ
            </span>
            <span class="card-dilivery-text">Гарантия качетсва продукции</span>
            <span class="card-dilivery-text">
              Бесплатная доставка от 3000 ₽
            </span>
          </v-row>
          <v-row>
            <span class="company-info start">
              © kitchin, 2024 BarNeo Professional (v. 3.384)
            </span>
          </v-row>
          <v-row>
            <span class="company-info">
              Профессиональное оборудование для ресторанов, кафе, баров,
              общепита.
            </span>
          </v-row>
        </v-col>
        <v-col class="right">
          <div class="item-info-container">
            <p class="collection-info">kuroi</p>
            <p class="title">Тарелка «Сундо», 12 см</p>
            <p class="price">2 000 ₽</p>
            <p class="desc">
              Тарелка выполнена из прочного материала, который позволит Вам
              всегда наслаждаться трапезой вместе с нашим товаром. Тарелка
              «Сундо» отлично подойдет для сервировки плотных блюд.
            </p>
            <button class="folder-button">добавить в коризну</button>
            <p></p>
            <button class="all-button">
              просмотреть все товары из коллекции
            </button>
          </div>
        </v-col>
      </v-row>
    </VContainer>
  </VLayoutDefault>
</template>

<style scoped>
.all-button {
  margin-top: 100px;
  background-color: transparent;
  border: 0.5px solid black;
  padding: 10px;
  font-family: "Montserrat", sans-serif;
  cursor: pointer;
  font-weight: 300;
  font-size: 15px;
}

.folder-button {
  background-color: black;
  border: none;
  padding: 10px;
  color: white;
  font-size: 15px;
  font-weight: 300;
  cursor: pointer;
  font-family: "Montserrat", sans-serif;
}

.desc {
  margin-top: 20px;
  font-size: 15px;
  margin-bottom: 60px;
}

.price {
  font-weight: 200;
  font-size: 25px;
}

.title {
  font-size: 23px;
  font-weight: 600;
  margin-bottom: 20px;
}

.collection-info {
  font-style: italic;
  font-size: 20px;
}

.company-info {
  font-size: 13px;
  font-weight: 300;
  margin-left: 70px;
  margin-top: 10px;
}

.company-info.start {
  margin-top: 40px;
}

.card-dilivery-text {
  font-size: 15px;
  font-weight: 200;
  width: 180px;
}

.card-dilivery-info {
  margin-top: 100px;
  margin-left: 70px;
}

.main {
  padding-top: 40px;
  padding-bottom: 70px;
  background-color: white;
}
.left {
  flex: 3;
}
.right {
  flex: 2;
  display: flex;
  align-items: center;
}
.back-button {
  border: none;
  background-color: transparent;
  margin-left: 70px;
  cursor: pointer;
}
.image-container {
  margin-top: 100px;
}
</style>
