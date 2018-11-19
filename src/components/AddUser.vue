<template>
  <form @submit.prevent="addUser">
    <input type="text" placeholder="Имя" v-model="user.name"/>
    <input type="text" placeholder="Фамилия" v-model="user.surname"/>
    <button>Добавить</button>
  </form>
</template>

<script>
export default {
  name: "AddUser",
  data: () => ({
    user: {      
      name: "",
      surname: ""
    }
  }),
  methods: {
    addUser() {
      if (!this.user.name || !this.user.surname) return;
      
      this.$emit("addUser", Object.assign({}, this.user));
    }
  }
}
</script>

<style lang="stylus" scoped>
button {
  margin: 0 8px;
  padding: 0 15px;
  height: 32px;
  background-color: #48CFAD;
  border: none;
  border-radius: 4px;
  font-weight: 700;
  color: #fff;
  box-shadow: none;
  cursor: pointer;
  transition: 0.3s;

  &:hover {
    background-color: #70dbbd;
  }
}

input {
  margin: 0 8px;
  padding: 4px 11px;
  height: 32px;
  border: 1px solid #d9d9d9;
  border-radius: 4px;
  color: #595959;
  transition: 0.3s;

  &:hover {
    border-color: #48CFAD;
  }

  &:focus {
    outline: none;
    border-color: #48CFAD;
    box-shadow: 0 0 0 2px rgba(72, 207, 173, 0.2);
  }
}
</style>
