<script lang="ts">
  import axios from 'axios'

  interface Joke {
    jokeId: number,
    joke: string,
    category: string
  }

  export default {
    data() {
      return {
        jokes: [] as Joke[],
        isButtonDisabled: false
      }
    },

    methods: {
      async getAllJokes() {
        fetch('https://v2.jokeapi.dev/joke/Programming?type=single&amount=10')
          .then((res) => res.json())
          .then(data => {
            this.jokes = data.jokes
            console.log(data.jokes)
          })
          .catch(error => console.log(error.message))
      },
      
      addFavoriteJoke(joke: Joke) {
        axios.post(`http://localhost:3004/jokes`, joke)
          .then((response) => console.log('the response is: ', response))
          .catch(error => console.log(error))
        alert('Joke added to favorites :)')
        this.isButtonDisabled = true
      }
    },

    mounted() {
      this.getAllJokes()
    }
  }
</script>

<template>
  <main class="home__container">
    <h1 class="home__heading">
      Funny jokes
    </h1>
    <div class="joke__container">
      <div 
        v-for="joke in jokes" 
        :key="joke.jokeId"
        class="joke_card"
      >
        <div class="joke__card--head">
          <button
            class="button__add"
            :disabled="isButtonDisabled"
            @click=addFavoriteJoke(joke)
          >
            Add to favorites &#x1F9E1
          </button>
          <span class="joke__category">
            {{ joke.category }}
          </span>
        </div>
        <p class="joke__content">
          {{ joke.joke }}
        </p>
      </div>
    </div>
  </main>
</template>

<style>
  .home__container {
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 20px;
    padding: 40px;
    padding-top: 10px;
  }

  .home__heading {
    text-align: center;
    font-size: 4rem;
    padding: 10px;
    font-family: 'Rubik Iso', cursive;
    text-shadow: 6px 6px 0px rgba(122, 80, 3, 0.2);
  }

  .joke__container {
    width: 90%;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  .joke_card {
    padding: 20px;
    border: 3px solid gray;
    background-color: var(--vt-c-secondary-base);
    color: var(--vt-c-content-secondary);
    border-radius: 0 30px;
    display: flex;
    flex-direction: column;
  }

  .joke__card--head {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .button__add {
    border: 3px solid var(--vt-c-secondary-accent);
    background-color: var(--vt-c-content-secondary);
    padding: 5px 10px;
    border-radius: 0 15px;
    cursor: pointer;
    font-family: 'Shantell Sans', cursive;
  }

  .joke__category {
    background-color: var(--vt-c-secondary-accent);
    color: var(--vt-c-content);
    padding: 10px 20px;
    border-radius: 0 15px;
  }

  .joke__content {
    padding: 10px;
  }

</style>