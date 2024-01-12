<template>
  <h1>Puntaje: {{ puntaje }}</h1>
  <h1>intento: {{ intento }}</h1>
  <div class="container">
    <Game
      ref="game1"
      url="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg"
      @txt="actualizarPuntaje"
    />
    <Game
      ref="game2"
      url="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/2.svg"
      @txt="actualizarPuntaje"
    />
    <Game
      ref="game3"
      url="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/3.svg"
      @txt="actualizarPuntaje"
    />
  </div>
  <button @click="jugar" :disabled="intento >= 5">{{ txtButton }}</button>
</template>

<script>
import Game from "./components/Game.vue";

export default {
  name: "App",
  components: {
    Game,
  },
  data() {
    return {
      puntaje: 0,
      intento: 0,
      txtButton: "Jugar",
    };
  },
  methods: {
    async jugar() {
      if (this.intento < 5) {
        this.intento++;
        await this.$refs.game1.consumirAPI();
        await this.$refs.game2.consumirAPI();
        await this.$refs.game3.consumirAPI();
      } else {
        this.txtButton = "Intentos Agotados";
      }
    },
    actualizarPuntaje(txt) {
      if (txt === "yes") {
        this.puntaje += 1;
      } else if (txt === "yes yes") {
        this.puntaje += 2;
      } else if (txt === "yes yes yes") {
        this.puntaje += 5;
      }
    },
  },
};
</script>
F

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  display: grid;
  justify-content: center;
  align-items: center;
  grid-template-columns: repeat(3, 1fr);
}
</style>
