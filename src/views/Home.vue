<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search</label>
      <form v-on:submit.prevent="getResult(searchValue)">
        <input id="search" name="search" v-model="searchValue" />
      </form>

      <ul>
        <li v-for="item in results" :key="item.data[0].nasa_id">
          <p>{{item.data[0].description}}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
      searchValue: "",
      results: []
    };
  },
  methods: {
    getResult(searchValue) {
      axios
        .get(
          "https://images-api.nasa.gov/search?q=" +
            searchValue +
            "&media_type=image"
        )
        .then(response => {
          this.results = response.data.collection.items;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.wrapper {
  margin: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}

.search {
  display: flex;
  flex-direction: column;
  width: 200px;
  font-size: 20px;

  input {
    height: 30px;
    border: 0;
    border-bottom: 1px solid black;
    font-size: 20px;
  }
}
</style>
