<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <Joke v-for="joke in jokes" :key="joke.id" :id="joke.id" :joke="joke.joke" />
  </div>
</template>
<script>
import axios from "axios";
import Joke from "./../../components/Joke";
import SearchJokes from "./../../components/SearchJokes";
export default {
  data() {
    return {
      jokes: [],

    };
  },
  components: { Joke , SearchJokes},
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get("https://icanhazdadjoke.com/search", config);
      //console.log(res.data)
      this.jokes = res.data.results;
    } catch (error) {
      console.log(error);
    }
  },
  head() {
    return {
      title: "Dad Jokes",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "best place for corny dad jokes"
        }
      ]
    };
  },
  methods: {
  async searchText(text){
      const config = {
        headers: {
            Accept: "application/json"
         }
        }
        try {
          const res = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`, config);
          //console.log(res.data)
          this.jokes = res.data.results;
        } catch (error) {
          console.log(error);
        }
      }
  },
};
</script>

<style lang="stylus" scoped></style>