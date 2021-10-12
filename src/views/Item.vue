<template>
  <div class="container  ">
    <div class="itens__margem-item">
    <router-link class="item__link-back  d-flex " to="/">
    <i class="fas fa-chevron-left"></i>
  <div class="col-md-2 item__title"> {{cards.title}}</div>
   </router-link>
  <div id="carouselExampleControls" class="carousel slide col-11" data-bs-ride="carousel">
  <div class="carousel-inner">
    <div class="carousel-item active">
      <img src="@/assets/images/chairs2.jpg" class="d-block w-100" alt="...">
    </div>
    <div class="carousel-item">
      <img src="@/assets/images/study2.jpg" class="d-block w-100" alt="...">
    </div>
 
  </div>
  <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleControls" data-bs-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Previous</span>
  </button>
  <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleControls" data-bs-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Next</span>
  </button>
</div>
<p class="item__text col-md-9 col-11">{{cards.text2}}</p>
<div class="d-flex align-items-center mb-5">
<div class="item__simbol">R$</div>
<div class="item__price ">
  
{{cards.price | itemPrice}}
</div>
<button class="button__item">
Habilitar
</button>
</div>
</div>


    </div>  
</template>

<script>
import { api } from "@/services.js";
export default {
  name: "Item",
  props: ["id"],
  data() {
      return {
          cards: null
      }
  },
  filters: {
    itemPrice(value) {
      return `${value},00`
    }
  },
  methods: {
    getCards() {
      api.get(`/cards/${this.id}`).then((response) => {
        this.cards = response.data;
      });
    },
  },
  created() {
    this.getCards();
  },
};
</script>

<style scoped>
.carousel-item  img{
  max-width: 1200px;
  
}

</style>
