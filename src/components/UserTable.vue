<template>
  <table>
    <thead>
      <tr>
        <th>№</th>
        <th @click="sortUsers(`name`)">Имя</th>
        <th @click="sortUsers(`surname`)">Фамилия</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(user, idx) in users" :key="idx">
        <td v-text="idx + 1"></td>
        <td v-text="user.name"></td>
        <td v-text="user.surname"></td>
      </tr>
    </tbody>
  </table>  
</template>

<script>
export default {
  name: "UserTable",
  props: {
    users: {
      type: Array,
      required: true
    }
  },
  methods: {
    sortUsers (name) {
      this.$emit("sortUsers", name)
    }
  }  
}
</script>

<style lang="stylus" scoped>
table {
  border-collapse: collapse;
  border-radius: 4px 4px 0 0;
  text-align: left;
}

th {
  padding: 16px;
  background-color: #fafafa;
  border-bottom: 1px solid #e8e8e8;
  user-select: none;
  cursor: pointer;
  transition: 0.3s;

  &:hover {
    color: #32a88f;
  }
}

td {
  padding: 16px;
  border-bottom: 1px solid #e8e8e8;
}
</style>


