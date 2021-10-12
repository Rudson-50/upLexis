<template>
  <div class="container itens__margem-principal">
    <div class="row">
    <div
      class="item__principal col-md-1 col-4"
      v-for="(item, index) in items"
      :key="item"
    >
      <button class="button__order" @click="onClick(words[index])">
        <i class="button__icon" :class="item"></i>
        <div>{{ words[index] }}</div>
      </button>
    </div>
    </div>
    <div class="text-center row">
      <div class="select col-md-2">
        <label for="select__label " class="select__label">ORDENAR</label>
        <select class="form-select " id="select__label" @change="selectVal($event)">
          <option v-for="(select, index) in selects" :key="index">{{select.value}}</option>
         
        </select>
      </div>
    </div>

    <div class="cards__margem text-center row">
      <div
        v-for="(card, id) in filterProducts"
        :key="id"
        class="col-md-3 col-12"
      >
        <div class="cards__body">
          <i class="cards__icon" :class="card.icon"></i>
          <div class="cards__title">{{ card.title }}</div>
          <div class="cards__text">{{ card.text }}</div>
        </div>
        <div class="cards__footer ">
          <div class="cards__price">{{ card.price | numberPrice }}</div>
          <router-link
            class="cards__link"
            :to="{ name: 'item', params: { id: card.id } }"
          >
            <div class="cards__about">Saiba mais</div>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { api } from "@/services.js";
export default {
  data() {
    return {
      cards: null,
      filterBy: "",
      items: [
        "fas fa-globe",

        "fas fa-briefcase",

        "fas fa-landmark",

        "fas fa-tree",

        "fas fa-gavel",

        "fas fa-ban",

        "fas fa-globe-americas",

        "fas fa-gem",
        "fas fa-male",

        "fas fa-piggy-bank",
      ],
      words: [
        "Todos",
        "Profissional",
        "Reguladores",
        "Sócio Ambiental",
        "Jurídico",
        "Listas Restritivas",
        "Mídia / Internet",
        "Bens e Imóveis",
        "Cadastro",
        "Financeiro",
      ],
      selects: [
            {value: 'Selecione'},
            {value: 'Lançamento'},
            {value: 'Preço'}
        ]
    };
  },
  methods: {
    getCards() {
      api.get("/cards").then((response) => {
        this.cards = response.data;
      });
    },
    onClick(text) {
      this.filterBy = text;
    },
    selectVal: function(ele) {

            if(ele.target.selectedIndex === 2) {
              this.cards.sort((a, b) => a.price < b.price ? 1 : -1) 
            }
            if(ele.target.selectedIndex === 1) {
              this.cards.sort((a, b) => new Date(a.date) - new Date(b.date))
            } 
          

        },
  },
  computed: {
    filterProducts() {
      if (this.filterBy === "") return this.cards;
      else if (this.filterBy === "Todos") return this.cards;
      else return this.cards.filter((card) => card.title === this.filterBy);
    },
  },
  filters: {
    numberPrice(valor){
      return valor.toLocaleString("pt-BR", {style: "currency", currency: "BRL"});
    }
    
  },
  created() {
    this.getCards();
  },
};
</script>

<style>

</style>
