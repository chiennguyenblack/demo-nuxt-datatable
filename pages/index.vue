<template>
  <div class="container">
    <h1>Search Page</h1>
    <div class="wrapper-search-bar">
      <div class="wrapper-search-input">
        <input type="text" v-model="searchText" @input="onInput" placeholder="Search...">
        <span class="icon" v-if="showClearIcon" @click="clearInput">
          ×
        </span>
      </div>
      <button class="btn-filter" @click="toggle('az')"> {{ status('az') }}</button>
      <button class="btn-filter" @click="toggle('ad')"> {{ status('ad') }}</button>
    </div>

    <div class="wrapper-list-item">
      <ul>
        <li v-for="item in filteredItems" :key="item.id">
          <div class="wrapper-item">
            <div class="wrapper-avatar">
              <img src="../static/default-avatar-profile.jpg" alt="">
            </div>
            <div class="wrapper-info">
              <h2>{{ item.name }}</h2>
              <p>{{ item.address }}</p>
              <label class="category">{{ item.category }}</label>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

import data from '../utils/db.json'
export default {
  data() {
    return {
      searchText: "",
      items: [],
      filterAZ: false,
      filterAddress: false,
    };
  },
  computed: {
    filteredItems() {
      const searchText = this.searchText.toLowerCase();

      // handle filter with search string
      let newList = this.items.filter(
        (item) =>
          item.name.toLowerCase().includes(searchText) ||
          item.address.toLowerCase().includes(searchText)
      );

      // handle sort a-z with key name and address( priority: name >> address)
      // apply sort name
      if(this.filterAZ && !this.filterAddress)
        return newList.sort((a, b) => a.name.localeCompare(b.name));

      // apply sort name and address
      if(this.filterAZ && this.filterAddress)
        return newList.sort((a, b) => {
          const nameCompare = a.name.localeCompare(b.name);
          if (nameCompare !== 0) {
            return nameCompare;
          }
          return a.address.localeCompare(b.address);
        });
      // apply sort address
      if(!this.filterAZ && this.filterAddress)
        return newList.sort((a, b) => a.address.localeCompare(b.address));

      return newList;
    },
    showClearIcon() {
      return this.searchText.length > 0;
    }
  },
  methods: {
    toggle(params) {
      if(params === 'az')
        this.filterAZ = !this.filterAZ;
      if(params === 'ad')
        this.filterAddress = !this.filterAddress;
    },
    status(name) {
      if(name === 'az')
        return this.filterAZ ? "A-Z On" : "A-Z Off";
      if(name === 'ad')
        return this.filterAddress ? "Address On" : "Address Off";
    },
    onInput(event) {
      this.searchText = event.target.value;
    },
    clearInput() {
      this.searchText = '';
    },
  },
  mounted() {
    this.items = data;
  }
};
</script>

<style lang="scss">
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

h1 {
  font-size: 24px;
  margin-bottom: 10px;
}

input[type="text"] {
  padding: 5px;
  border-radius: 5px;
  border: none;
  font-size: 16px;
  outline: none;
  width: 85%;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

li {
  background-color: #fff;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
  width: 100%;
  max-width: 600px;
}

h2 {
  font-size: 18px;
  margin-bottom: 0px;
  margin-top: 0px;
}

p {
  font-size: 14px;
  margin-bottom: 0px;
  margin-top: 0px;
}

.wrapper-list-item{
  height: 500px;
  width: 80%;
  overflow-y: scroll;
}

.wrapper-item{
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 10px;
  margin-bottom: 10px;
}

.wrapper-avatar{
  border-radius: 50%;
  width: 50px;
  height: 50px;
  display: flex;
}
.wrapper-avatar img{
  border-radius: 50%;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.category{
  border: 1px solid #ccc;
  border-radius: 10px;
  font-size: small;
  padding: 2px 5px;
}

.btn-filter{
  background-color: darkcyan;
  color: #fff;
  border: 1px solid darkcyan;
  padding: 2px 5px;
  border-radius: 2px;
  margin: 0px 5px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
}
.wrapper-search-bar{
  display: flex;
  flex-direction: row;
  margin: 20px 0px;
  width: 80%;
  justify-content: space-between;
}

.wrapper-search-input {
  position: relative;
  border: 1px solid darkcyan;
  border-radius: 5px;
  margin-right: 10px;
  width: 70%;
}
.icon {
  position: absolute;
  right: 8px;
  top: 5px;
  color: black;
  cursor: pointer;
  font-weight: 700;
}
</style>
