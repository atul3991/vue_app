<template>
  <span class="autocomplete">
    <input type="text" v-model="search" @input="onChange" />
    <ul class="autocomplete-results" v-show="isOpen">
      <li v-for="(result, i) in results" :key="i" class="autocomplete-result" @click="setResult(result)">
          {{result}}
      </li>
    </ul>
  </span>
</template>

<script>
  export default {
    props: {
      items: {
        type: Array,
        required: false,
        default: () => [],
      },
    },
    data() {
      return {
        search: '',
        results: [],
        isOpen: false
      };
    },
    methods: {
      onChange() {
        this.isOpen = true;
        this.filterResults();
        this.$emit('update:search', this.search);
      },
      filterResults() {
        this.results = this.items.filter(item => item.toLowerCase().indexOf(this.search.toLowerCase()) > -1);
      },
      setResult(result) {
        this.search = result;
        this.isOpen = false;
        this.$emit('update:search', this.search);
      }
    }
  };
</script>
<style>
  .autocomplete {
    position: relative;
    width: 130px;
  }

  .autocomplete-results {
    padding: 0;
    margin: 0;
    border: 1px solid #eeeeee;
    height: 120px;
    overflow: auto;
  }

  .autocomplete-result {
    list-style: none;
    text-align: left;
    padding: 4px 2px;
    cursor: pointer;
  }

  .autocomplete-result:hover {
    background-color: #4AAE9B;
    color: white;
  }
</style>