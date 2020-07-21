<template>
  <div class="hello">
    <ul>
      <li v-for="item in cell" :key="item.id" class="wiki__item">
        <i title="Unselect option" @click.stop="unselectOption(option)">×</i>
        <span>{{ item.lang }}</span>
      </li>
      <li class="multi-select__input" ref="textInputContainer">
        <input
          type="text"
          :placeholder="hasSelected ? '' : placeholder"
          :title="title"
          v-model="caption"
          @keydown="
            toggleDropDown(true, true);
            updateTextInputWidth();
          "
          @keydown.enter="trySelectOption()"
          @keydown.up="hoverNextOption(false)"
          @keydown.down="hoverNextOption(true)"
          @keydown.esc="toggleDropDown(false, false)"
        />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'WikiA',

  data() {
    return {
      caption: '',
      lang: '',
      open: true,
      valueCategory: [],
      cell: [
        { id: 1, lang: 'Русский' },
        { id: 2, lang: 'Английский' },
        { id: 3, lang: 'Абхазский' },
        { id: 4, lang: 'Аври' },
      ],
    };
  },
  props: {
    msg: String,
    placeholder: {
      type: String,
      default: '',
    },
    // Text input hint message
    title: {
      type: String,
      default: '',
    },
  },
  methods: {
    findSelected(option) {
      for (let pos in this.selectedOptions) {
        if (
          this.selectedOptions.hasOwnProperty(pos) &&
          this.selectedOptions[pos].id === option.id
        ) {
          return Number.parseInt(pos);
        }
      }
      return -1;
    },
    sortVal() {
      let _val = this.item;
      let _cel = this.cell;
      _cel.map(i => {
        let _k = i.lang;
        if (_k.toLowerCase().includes(_val)) {
          this.valueCategory.push(_k);
        }
      });
    },
  },
  watch: {
    change() {
      console.log(this.valueCategory.length);
    },
  },
  computed: {
    events() {
      return {
        DROP_DOWN_SHOW: 'drop-down-show',
        DROP_DOWN_HIDE: 'drop-down-hide',
        OPTIONS_LOADED: 'options-loaded',
      };
    },

    hasSelected() {
      return (
        Array.isArray(this.selectedOptions) && this.selectedOptions.length > 0
      );
    },
  },
};
</script>

<style lang="scss" scoped>
$mobile-width: 320px;
$color: green;
.wiki {
  display: flex;
}
.wiki__lang {
  box-sizing: border-box;
  width: 300px;
  margin: 0 auto;
  background-color: #fff;
  color: #55677d;
  border: 1px solid blue;
}
.wiki__item {
  display: inline-block;
  border: 1px solid green;
  width: 250px;
  height: 70px;
  margin-bottom: 5px;
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
