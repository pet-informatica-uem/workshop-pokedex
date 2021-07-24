<template>
  <div class="container">
    <main class="text-center">
      <div class="logo my-5" @click="clear_all">
        <img src="../assets/pokedex-logo.svg" alt="Pokédex" />
      </div>
      <div class="search">
        <b-form-input
          type="text"
          placeholder="Digite o nome ou ID de um pokémon"
          class="my-4"
          v-model="pokemon_name"
          @keyup.enter="search"
        />
        <b-button variant="warning" @click="search" size="lg">Buscar</b-button>
      </div>
    </main>
    <div class="result">
      <div
        v-show="loading"
        class="loading justify-content-center align-items-center"
      >
        <b-spinner label="Spinning" variant="white" size="lg"></b-spinner>
      </div>
      <div
        v-show="error && !loading"
        class="error_message justify-content-center align-items-center"
      >
        <h2>
          Pokémon <span>{{ pokemon_error_name }}</span> não encontrado
        </h2>
      </div>
      <div v-if="pokemon.id && !loading">
        <div class="divider d-flex justify-content-center align-items-center ">
          <h2 class="text-center mx-4">RESULTADO</h2>
        </div>
        <div
          :style="color_accent"
          class="card d-flex flex-row p-5 justify-content-between"
        >
          <div class="name d-flex flex-column justify-content-between">
            <div class="info">
              <h2>
                {{ pokemon.name }} Nº
                {{ pokemon.id.toString().padStart(3, "0") }}
              </h2>
              <span class="px-3 py-1 mt-3">{{ pokemon.type }}</span>
            </div>
            <div class="measures d-flex align-center justify-content-between">
              <div
                class="d-flex justify-content-center align-items-center weight"
              >
                <img
                  class="icon"
                  src="../assets/balance.svg"
                  alt="Weigth"
                  width="48"
                />
                <span class="ml-3">{{ pokemon.weight }} Kg</span>
              </div>
              <div
                class="d-flex justify-content-center align-items-center height"
              >
                <img
                  class="icon"
                  src="../assets/ruler.svg"
                  alt="Height"
                  height="48"
                />
                <span class="ml-3">{{ pokemon.height }} m</span>
              </div>
            </div>
          </div>
          <div class="separator d-flex"></div>
          <div
            class="attributes d-flex flex-column align-items-start justify-content-between"
          >
            <div class="d-flex justify-content-center">
              <img src="../assets/heart.svg" alt="HP" width="36" class="icon" />
              <span class="ml-3">{{ pokemon.health }} HP</span>
            </div>
            <div class="d-flex justify-content-center">
              <img
                src="../assets/sword.svg"
                alt="Attack"
                width="36"
                class="icon"
              />
              <span class="ml-3">{{ pokemon.attack }} ATK</span>
            </div>
            <div class="d-flex justify-content-center">
              <img
                src="../assets/shield.svg"
                alt="Defense"
                width="36"
                class="icon"
              />
              <span class="ml-3">{{ pokemon.defence }} DEF</span>
            </div>
            <div class="d-flex justify-content-center">
              <img
                src="../assets/speed.svg"
                alt="Speed"
                width="36"
                class="icon"
              />
              <span class="ml-3">{{ pokemon.speed }} SPD</span>
            </div>
          </div>
          <div class="image">
            <img :src="pokemon.sprite" :alt="pokemon.name" width="200" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pokemon_error_name: "",
      pokemon_name: "",
      pokemon: {},
      error: false,
      loading: false
    };
  },
  methods: {
    async search() {
      try {
        this.loading = true;
        const res = await fetch(
          `https://pokeapi.co/api/v2/pokemon/${this.pokemon_name.toLowerCase()}`
        );

        const body = await res.json();

        this.pokemon = {
          id: body.id,
          name: body.name.toUpperCase(),
          weight: body.weight,
          height: body.height,
          health: body.stats[0].base_stat,
          attack: body.stats[1].base_stat,
          defence: body.stats[2].base_stat,
          speed: body.stats[5].base_stat,
          type: body.types[0].type.name.toUpperCase(),
          sprite: body.sprites.other["official-artwork"].front_default
        };
        this.error = false;
      } catch (err) {
        this.pokemon = {};
        this.error = true;
        this.pokemon_error_name = this.pokemon_name;
      } finally {
        this.pokemon_name = "";
        this.loading = false;
      }
    },
    clear_all() {
      this.pokemon_error_name = "";
      this.pokemon_name = "";
      this.pokemon = {};
      this.error = false;
      this.loading = false;
    }
  },
  computed: {
    color_accent() {
      const typeColors = {
        normal: "#A8A878",
        fire: "#F08030",
        water: "#6890F0",
        grass: "#78C850",
        electric: "#F4C430",
        ice: "#98D8D8",
        fighting: "#C03028",
        poison: "#A040A0",
        ground: "#E0C068",
        flying: "#A890F0",
        psychic: "#F85888",
        bug: "#A8B820",
        rock: "#B8A038",
        ghost: "#705898",
        dark: "#705848",
        dragon: "#7038F8",
        steel: "#B8B8D0",
        fairy: "#F0B6BC"
      };
      return {
        "background-color": typeColors[this.pokemon.type?.toLowerCase()]
      };
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Livvic:wght@700&family=Red+Rose&display=swap");

:root {
  --bg-color: #29292e;
  --red: #ef4036;
  --yellow: #ffcb05;
  --text-color: #595959;
  --result-text: #ccc;
  --white: #f8f8f8;
}

body {
  font-family: "Red Rose", sans-serif;
  background-color: var(--bg-color);
}

.container main {
  width: 100%;
  max-width: 1029px;
}

.logo img {
  width: 100%;
  max-width: 642px;
  cursor: pointer;
}

.search input {
  font-size: 2.25rem;
  color: var(--text-color);
  border-radius: 16px;
  text-align: center;
}

.search input::placeholder {
  text-align: center;
}

.search input:focus {
  border-color: var(--red);
  box-shadow: 0 0 0 0.1rem rgba(239, 64, 54, 0.5);
}

.search button {
  font-weight: bold;
  font-size: 2.25rem;
  color: var(--text-color);
  padding: 0.3rem 1.5rem;
  border-radius: 16px;
}

.result {
  width: 100%;
  max-width: 1029px;
  margin-top: 48px;
}

.result h2 {
  font-size: 2.25rem;
  color: var(--result-text);
}

.card {
  color: var(--white);
  border-radius: 16px;
}

.name {
  flex: 0.6;
}

.name .info h2 {
  font-family: "Livvic", sans-serif;
  font-size: 2.25rem;
  font-weight: bold;
  color: var(--white);
}

.name .info span {
  background-color: rgba(255, 255, 255, 0.25);
  width: fit-content;
  font-size: 1.5rem;
  border-radius: 32px;
}

span {
  font-size: 1.5rem;
}

.error_message {
  display: flex;
}

.error_message span {
  font-size: inherit;
  color: var(--red);
}

.divider::before {
  content: "";
  height: 2px;
  background-color: var(--text-color);
  flex: 1;
}
.divider::after {
  content: "";
  height: 2px;
  background-color: var(--text-color);
  flex: 1;
}

.image {
  background-color: var(--white);
  border-radius: 16px;
  padding: 16px;
}

.loading {
  min-height: 300px;
  display: flex;
}

.loading span {
  height: 64px;
  width: 64px;
}

.separator::before {
  content: "";
  width: 3px;
  border-radius: 16px;
  background-color: rgba(255, 255, 255, 0.25);
}

@media (max-width: 991px) {
  html {
    font-size: 75%;
  }

  .card {
    flex-direction: column !important;
  }

  .name {
    flex-direction: row !important;
  }

  .icon {
    width: 32px;
    height: 32px;
  }

  .measures {
    gap: 2rem;
  }

  .measures .height {
    margin-right: 2.5rem;
  }

  .measures .weight {
    margin-right: 4.5rem;
  }

  .attributes {
    flex-direction: row !important;
    margin: 2rem 0;
  }

  .image {
    text-align: center;
  }
}

@media (max-width: 767px) {
  html {
    font-size: 62%;
  }

  .measures .height {
    margin-right: 2rem;
  }

  .measures .weight {
    margin-right: 2.2rem;
  }

  .attributes {
    flex-wrap: wrap;
    gap: 2rem;
  }

  .icon {
    width: 24px;
    height: 24px;
  }
}

@media (max-width: 480px) {
  .card {
    margin-top: 1rem;
  }

  .name {
    flex-direction: column !important;
  }

  .measures {
    margin-top: 2rem;
  }
}
</style>
