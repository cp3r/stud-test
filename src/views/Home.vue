<template>
  <div class="home">
    <AddUser @addUser="addUser" />    
    <label>
      Количество пользователей на странице:
      <select v-model="usersOnPage">
        <option>3</option>
        <option>4</option>
        <option>5</option>
        <option>6</option>
        <option>7</option>
        <option>8</option>
        <option>9</option>
        <option selected>10</option>
      </select>
    </label>
    <UserTable :users="filtredUsers" @sortUsers="sortUsers"/>
    <Pagination :pages="pages" :currentPage="currentPage" @changePage="changePage"/>        
  </div>
</template>

<script>
import AddUser from "@/components/AddUser.vue";
import UserTable from "@/components/UserTable.vue";
import Pagination from "@/components/Pagination.vue";

export default {
  name: "home",
  components: {
    AddUser,
    UserTable,
    Pagination
  },
  data: () => ({
    users: [{
      name: "Петр", 
      surname: "Васильев"
    },
    {
      name: "Александр", 
      surname: "Зобнин"
    },
    {
      name: "Мария", 
      surname: "Стрельникова"
    },
    {
      name: "Антон", 
      surname: "Рожков"
    },
    {
      name: "Светлана", 
      surname: "Синицина"
    }],
    sortDirections: ["none", "asc", "desc"],
    sortField: "",
    sortDirection: "none",
    usersOnPage: 10,
    currentPage: 1
  }),
  methods: {
    addUser(user) {
      this.users.push(user);
    },
    sortUsers(field) {
      let idx = this.sortDirections.indexOf(this.sortDirection);
      let nextDir = this.sortDirections[idx + 1];

      if (this.sortField === field) {
        this.sortDirection = nextDir ? nextDir : this.sortDirections[0];
      } else {
        this.sortDirection = this.sortDirections[1];
      }
      
      this.sortField = field;      
    },
    changePage (step) {
      let newPage = this.currentPage + step;
      this.setCurrentPage(newPage);
    },
    setCurrentPage(page) {
      if (page >= 1 && page <= this.pages) {
        this.currentPage = page;
      }
    }
  },
  computed: {
    pages () {
      return Math.ceil(this.users.length / this.usersOnPage);
    },
    sortedUsers () {
      if (this.sortDirection === "none") return this.users;
      
      let m = this.sortDirection === "asc" ? 1 : -1;

      return this.users.slice().sort((a, b) => {
        return a[this.sortField] > b[this.sortField] ? 1 * m : -1 * m;
      })
    },
    filtredUsers () {
      let end = this.currentPage * this.usersOnPage;
      let start = end - this.usersOnPage;

      return this.sortedUsers.slice(start, end)
    }
  }
};
</script>

<style lang="stylus" scoped>
.home {
  padding: 16px;
}

label {
  display: block;
  margin: 16px 8px;
}

select {
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
