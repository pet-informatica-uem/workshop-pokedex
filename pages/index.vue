<template>
  <div class="container">
    <main class="text-center">
      <div class="logo my-5">
        <img src="../assets/pokedex-logo.svg" alt="Pokédex" />
      </div>
      <div class="search">
        <b-form-input
          type="text"
          placeholder="Digite o nome ou ID de um pokémon"
          class="my-4"
        />
        <b-button variant="warning" size="lg">Buscar</b-button>
      </div>
    </main>
    <div class="result">
      <h2 class="text-center">RESULTADO</h2>
      <div class="card d-flex flex-row p-5 justify-content-around">
        <div class="name">
          <div class="info">
            <h2>SQUIRTLE Nº007</h2>
            <p class="px-3 py-1 mt-3 mb-5">WATER</p>
          </div>
          <div class="measures d-flex align-center">
            <p class="mr-5">
              <img class="icon" src="../assets/balance.svg" alt="Weigth" />
              9.0 Kg
            </p>
            <p>
              <img class="icon" src="../assets/ruler.svg" alt="Height" />
              0.5 m
            </p>
          </div>
        </div>
        <div class="attributes">
          <p>
            <img class="icon" src="../assets/heart.svg" alt="HP" />
            44 HP
          </p>
          <p>
            <img class="icon" src="../assets/sword.svg" alt="Attack" />
            48 ATK
          </p>
          <p>
            <img class="icon" src="../assets/shield.svg" alt="Defense" />
            65 DEF
          </p>
          <p>
            <img class="icon" src="../assets/speed.svg" alt="Speed" />
            43 SPD
          </p>
        </div>
        <div class="image">
          <img src="../assets/squirtle.png" alt="Squirtle" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Livvic&family=Red+Rose:wght@400;700&display=swap");

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
}

.search input {
  font-size: 36px;
  color: var(--text-color);
  border-radius: 16px;
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
  font-size: 36px;
  color: var(--text-color);
  padding: 10px 75px;
  border-radius: 16px;
}

.result {
  width: 100%;
  max-width: 1029px;
  margin-top: 100px;
}

.result h2 {
  font-size: 36px;
  color: var(--result-text);
}

.card {
  background-color: #587acc;
  color: var(--white);
  border-radius: 16px;
}

.name .info h2 {
  font-family: "Livvic", sans-serif;
  font-size: 36px;
  font-weight: bold;
  color: var(--white);
}

.name .info p {
  background-color: #6890f0;
  width: fit-content;
  font-size: 24px;
  border-radius: 32px;
}

.card .icon {
  max-width: 36px;
}
</style>
