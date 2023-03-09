<script lang="ts">
  import axios from 'axios';

  interface FavoriteJoke {
    jokeId: number,
    joke: string 
  }

  export default {
    data() {
      return {
        jokes: [] as FavoriteJoke[]
      };
    },

    methods: {
      async getAllFavorites() {
         fetch('http://localhost:3004/jokes')
          .then((res) => res.json())
          .then(data => {
            this.jokes = data
            console.log(data)
          })
          .catch(error => console.log(error.message))
      },
      async removeFavorite(id: number) {
        console.log(123)
        await axios.delete(`http://localhost:3004/jokes/${id}`)
        .then(() => {
          this.jokes = this.jokes.filter((joke) => joke.jokeId !== id)
        })
        console.log(`Favorite with id ${id} removed.`);
      },
    },

    mounted() {
     this.getAllFavorites()
    }
  }
</script>

<template>
  <main class="favorite__container">
    <h1 class="favorite__heading">
      Your favorite jokes
    </h1>
    <div class="joke__container">
      <div 
        v-for="joke in jokes" 
        :key="joke.jokeId"
        class="joke_card"
      >
        <div class="joke__card--head">
          <button
            class="button_remove"
            @click=removeFavorite(joke.jokeId)
          >
            Remove
          </button>
        </div>
        <p class="joke__content">
          {{ joke.joke }}
        </p>
      </div>
    </div>
  </main>
</template>

<style>
   .favorite__container {
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 20px;
    padding: 40px;
    padding-top: 10px;
  }

  .favorite__heading {
    text-align: center;
    font-size: 2rem;
    padding: 10px;
    font-family: 'Rubik Iso', cursive;
    text-shadow: 6px 6px 0px rgba(122, 80, 3, 0.2);
  }

  .button_remove {
    background-color: var(--vt-c-secondary-accent);
    color: var(--vt-c-content);
    padding: 10px 15px;
    border-radius: 0 15px;
    border: 2px solid var(--vt-c-content-secondary);
    cursor: pointer;
    font-family: 'Shantell Sans', cursive;
  }
</style>
