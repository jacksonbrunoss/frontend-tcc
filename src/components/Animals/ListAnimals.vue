<template>
  <section class="list-animals">
    <div class="container">
      <div class="content">
        <transition mode="out-in">
          <div v-if="animals && animals.length" key="loop">
            <div class="content-animals">
              <Animals
                v-for="animal in animals"
                :key="animal.id"
                :id="animal.id_animal"
                :nome="animal.nome"
                :img="animal.imagem_animal"
                :sexo="animal.sexo"
                :id_users="animal.id_users"
                :tamanho="animal.tamanho"
                :cidade="animal.cidade"
                :estado="animal.estado"
              />
            </div>
            <div>
              <Pagination :animalsTotal="animalsTotal" :limit="limit" />
            </div>
          </div>
          <div v-else-if="animals && animals.length === 0" key="not">
            <p class="not">Busca sem resultados. Tente buscar outro termo.</p>
          </div>
          <div v-else key="load">
            <Loading />
          </div>
        </transition>
      </div>
    </div>
  </section>
</template>

<script>
import { api } from "@/services/services.js";
import { serialize } from "@/helpers/helpers.js";
import Animals from "./Animals.vue";
import Pagination from "./Pagination.vue";
export default {
  name: "ListAnimals",
  components: { Animals, Pagination },
  data() {
    return {
      animals: null,
      limit: 4,
      animalsTotal: 0
    };
  },
  computed: {
    url() {
      const query = serialize(this.$route.query);
      return `/animals/?_limit=${this.limit}${query}`;
    }
  },
  methods: {
    GetAnimals() {
      this.animals = null;
      api.get(this.url).then(res => {
        this.animals = res.data.animals;
        console.log(this.animals);
      });
    }
  },
  watch: {
    url() {
      this.GetAnimals();
    }
  },
  created() {
    this.GetAnimals();
  }
};
</script>

<style lang="scss" scoped>
.list-animals {
  width: 100%;
  margin-top: 4rem;
}
.content-animals {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 32px;
}
.not {
  color: var(--black-l);
  font-size: 1.15rem;
  text-align: center;
}
</style>
