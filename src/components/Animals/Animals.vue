<template>
  <router-link :to="{name: 'AnimalPage', params: {id: id} }">
    <div class="card-animals">
      <div class="img-card">
        <img v-if="img == null" src="@/assets/pic.jpg" alt="Ouve algum erro com essa imagem." />
        <img v-else :src="`http://localhost:3030/${img}`" :alt="nome" />
      </div>
      <div class="info">
        <h3>{{ nome }}</h3>
        <div class="sub-info">
          <div class="port-box">
            <div class="tamanho" :class="{ activep }">P</div>
            <div class="tamanho" :class="{ activem }">M</div>
            <div class="tamanho" :class="{ activeg }">G</div>
          </div>
          <span>
            <i v-if="sexo === 'macho'" class="bx bx-male-sign"></i>
            <i v-else class="bx bx-female-sign"></i>
          </span>
        </div>
      </div>
      <div class="local">{{cidade}}/{{estado}}</div>
    </div>
  </router-link>
</template>

<script>
export default {
  name: "Animals",
  props: [
    "img",
    "nome",
    "sexo",
    "id_users",
    "tamanho",
    "id",
    "cidade",
    "estado"
  ],
  data() {
    return {
      activep: false,
      activem: false,
      activeg: false
    };
  },
  methods: {
    setColor() {
      const tamanho = this.tamanho;
      tamanho === "pequeno" ? (this.activep = true) : (this.activep = false);
      tamanho === "medio" ? (this.activem = true) : (this.activem = false);
      tamanho === "grande" ? (this.activeg = true) : (this.activeg = false);
    }
  },
  created() {
    this.setColor();
  }
};
</script>

<style lang="scss" scoped>
.activep,
.activem,
.activeg {
  border: solid 2px var(--green-l) !important;
  color: var(--green-l) !important;
}
.card-animals {
  width: 100%;
  background: var(--light);
  border-radius: 3px;
  overflow: hidden;
  border: solid 1px var(--green-l);
  > .info {
    width: 100%;
    padding: 8px 8px;
    > h3 {
      font-size: 1.125rem;
      color: var(--blue);
      margin: 8px 0px;
      background: var(--gradient);
      background-clip: text;
      -webkit-text-fill-color: transparent;
      text-align: center;
      text-transform: uppercase;
      font-weight: 900;
    }
  }
  > .local {
    padding: 8px 8px;
    color: var(--black-l);
  }
  transition: 0.2s ease;
  &:hover {
    transform: scale(1.1);
    transition: 0.2s ease;
  }
}
.sub-info {
  width: 100%;
  justify-content: space-between;
  align-items: center;
  display: flex;
}
.img-card {
  width: 100%;
  height: 150px;
  overflow: auto;
  box-shadow: 0px 4px 0px 0px rgba(61, 204, 142, 2);
  > img {
    width: 100%;
    height: 100%;
  }
}
.port-box {
  display: flex;
  > .tamanho {
    border-radius: 3px;
    margin: 0px 8px 0px 0px;
    width: 30px;
    height: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
    border: solid 2px var(--black-l);
    text-transform: uppercase;
    font-weight: 800;
    color: var(--black-l);
  }
}

.bx-male-sign,
.bx-female-sign {
  color: var(--green-l);
  font-size: 1.5rem;
}
</style>
