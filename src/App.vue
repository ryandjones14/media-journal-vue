<template>
  <div id="app">
    <div class="media-types">
      <div class="media-type" v-for="type in mediaTypes" :class="{ selected: isTypeSelected(type.isSelected) }" :key="type.id" @click.stop="selectType(type.id)">
        {{ type.name }}
      </div>
    </div>
    <div class="selectedType" v-if="selectedType">
      {{ activeTypeName }}
      <input v-model="newTitle" placeholder="add a new title" @keyup.13="addTitle">
      <div v-if="selectedType.titles">
        <Titles :titles="selectedType.titles" />
      </div>
    </div>
  </div>
</template>

<script>
import Titles from './components/Titles.vue'

export default {
  name: 'app',
  components: {
    Titles
  },
  data: function () {
    return {
      selectedType: '',
      mediaTypes: [
        {
          id: 0,
          name: 'tv',
          titles: [],
          isSelected: false,
        },
        {
          id: 1,
          name: 'movie',
          titles: [],
          isSelected: false,
        },
        {
          id: 2,
          name: 'book',
          titles: [],
          isSelected: false,
        },
        {
          id: 3,
          name: 'podcast',
          titles: [],
          isSelected: false,
        },
        {
          id: 4,
          name: 'music',
          titles: [],
          isSelected: false,
        },
      ],
      newTitle: '',
    };
  },
  computed: {
    activeTypeName: function() {
      return this.selectedType.name;
    },
    
  },
  methods: {
    isTypeSelected: function(isSelected) {
      console.log('toggle isTypeSelected');
      return isSelected;
    },
    selectType: function (id) {
      let type = this.mediaTypes.find(type => type.id === id);
      type.isSelected = true;
      this.selectedType = type;
      window.setTimeout(() => {
        console.log('turn isSelected off');
        type.isSelected = false;
      }, '70');
    },
    addTitle: function(e) {
      const title = e && e.target && e.target.value;
      let selectedTypeTitlesCopy = [...this.selectedType.titles];
      selectedTypeTitlesCopy.push({title, id: selectedTypeTitlesCopy.length});
      // let type = this.mediaTypes.find(type => type.id === this.selectedTitle.id);
      this.mediaTypes[this.selectedType.id].titles = selectedTypeTitlesCopy;
      this.newTitle = '';
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.media-types {
  display: flex;
  justify-content: space-around;
}
.media-type {
  flex: 1 75px;
  height: 100px;
  max-width: 75px;
  background-color: #42b983;
  border: solid 1px black;
  transition: all .07s ease;
}
.selected {
  transform: scale(1.1);
  border-color: #ffc600;
  box-shadow: 0 0 1rem #ffc600;
}
</style>
