<template>
  <ul>
    <li>
      <button type="button" @click="changePage(-1)"><</button>
    </li>
    <li v-for="p in pages" :key="p" :class="{active: p === currentPage}">
      {{p}}
    </li>
    <li>
      <button type="button" @click="changePage(1)">></button>
    </li>
  </ul>
</template>

<script>
export default {
  name: "Pagination",
  props: {
    currentPage: {
      type: Number,
      required: true
    },
    pages: {
      type: Number,
      required: true
    }
  },
  methods: {
    changePage (step) {
      this.$emit("changePage", step);
    }
  }
}
</script>

<style lang="stylus" scoped >
ul {
  margin: 0;
  padding: 0;
  display: flex;
  list-style: none;
}

li {
  margin: 4px;
  width: 30px;
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid #d9d9d9;
  border-radius: 4px;
  color: #8C8C8C;
  cursor: pointer;
  transition: 0.3s;

  &.active {
    border-color: #48CFAD;
    color: #32a88f;
  }

  &:hover {
    border-color: #48CFAD;
    color: #32a88f;

    button {
      color: #32a88f;
    }
  }
}

button {
  width: 100%;
  height: 100%;
  background-color: transparent;
  border: none;
  color: #8C8C8C;
  cursor: pointer;
  transition: 0.3s;
}
</style>


