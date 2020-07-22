<template>
  <div class="hello">
    <div class="wiki__lang">
      <ul class="wiki__items">
        <label class="wiki__label" for="search">Язык:</label>
        <input
          class="wiki__search"
          @input="sortVal"
          @keydown.down="keyDown"
          @keydown.esc="closeSearch"
          type="text"
          v-model="search"
        />
        <button class="wiki__btn" @click="open = !open">C</button>

        <li
          class="wiki__item"
          v-show="open"
          v-for="item in sortVal"
          :key="item.id"
          @click="checkThis"
        >{{ item.lang }}</li>
        <ul class="wiki__check--items">
          <li class="wiki__check" v-for="lang in newArr" :key="lang.id" @click="delItem">{{lang}}</li>
        </ul>
      </ul>
    </div>

    <hr />
  </div>
</template>

<script>
export default {
  name: "multiSelect",

  data() {
    return {
      search: "",
      lang: "",
      open: false,
      newArr: [],
      cell: [
        { id: 1, lang: "Русский" },
        { id: 2, lang: "Английский" },
        { id: 3, lang: "Абхазский" },
        { id: 4, lang: "Аври" },
      ],
    };
  },

  methods: {
    checkThis(event) {
      this.newArr.push(event.target.textContent);
    },
    delItem(event) {
      this.newArr.splice(event.target.textContent, 1);
    },
    keyDown(e) {
      console.log(e.target);
    },
    closeSearch() {
      if (this.open === true) {
        this.open = !true;
      }
    },
  },
  computed: {
    sortVal() {
      return this.cell.filter((item) => {
        return item.lang.toLowerCase().includes(this.search.toLowerCase());
      });
    },
  },

  watch: {
    search: function setSearch() {
      if (this.search.length > 0) {
        this.open = true;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.wiki {
  display: flex;
}
.wiki__lang {
  box-sizing: border-box;
  width: 400px;
  margin: 0 auto;
  background-color: #fff;
  color: #55677d;
  border: 1px solid blue;
}
.wiki__items {
  position: relative;
}
.wiki__item {
  display: inline-block;
  border: 1px solid #dae2ea;
  width: 300px;
  height: 70px;
  margin-left: 61px;
  text-align: left;
  padding-top: 23px;
  padding-left: 5px;
  box-sizing: border-box;
  cursor: pointer;
  &:hover {
    background-color: #e5ebf1;
  }
}
.wiki__label {
  margin-right: 10px;
}
.wiki__search {
  box-sizing: border-box;
  width: 300px;
  height: 53px;
}
.wiki__btn {
  position: absolute;
  right: 23px;
  width: 27px;
  height: 53px;
  background-color: transparent;
  border: none;
  cursor: pointer;
}
.wiki__check--items {
  display: flex;
  justify-content: space-between;
  top: 0px;
  box-sizing: border-box;
  left: 73px;
  position: absolute;
}
.wiki__check {
  display: inline-block;
  padding: 3px;
  margin: 3px;
  background-color: #dae2e8;
  cursor: pointer;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
