<template>
  <div>
    <h1>My To Do List</h1>
    <input v-model="newItem">
    <button @click="addItemToList">Add</button>
    <ul>
      <li v-for="item in listItems" :key="item.id">{{ item.aciklama }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'List',
  data () {
    return {
      listItems: [],
      newItem: ''
    }
  },
  methods: {
    addItemToList () {
      const requestOptions = {
        method: 'POST',
        headers: {'Content-Type': 'application/json', 'Access-Control-Allow-Origin': '*'},
        body: JSON.stringify({aciklama: this.newItem})
      }
      fetch('https://todolist-backend-production.herokuapp.com/todo-control', requestOptions)
        .then(() => {
          fetch('https://todolist-backend-production.herokuapp.com/todo-control')
            .then(response => response.json())
            .then(data => {
              this.listItems = data
              this.newItem = ''
            })
        })
    }
  },
  created () {
    fetch('https://todolist-backend-production.herokuapp.com/todo-control')
      .then(response => response.json())
      .then(data => (this.listItems = data))
  }
}
</script>

<style scoped>

</style>
