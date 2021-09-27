<template>
    <div>
        <!-- now the time of design-->
        <h1 class="text-center my-4">Todo App</h1>
        <div class="container my-5">
            <div class="d-flex justify-content-center">
              <div v-if="editing" class="form-inline ">
                  <input class="form-control" type="text"  name="todo" v-model="todo" />
                  <button v-on:click="updateTodo()" class="btn btn-success ml-3">update</button>
              </div>
              <div v-else class="form-inline ">
                  <input class="form-control" type="text" name="todo" v-model="todo" />
                  <button v-on:click="addTodo()" class="btn btn-success ml-3">Add</button>
              </div>
            </div>
        </div>
      

        <div class="container">
          <div v-for="item in list" :key="item.id">
          <div class="card my-2">
            <div class="card-body d-flex justify-content-between">
            <h5>{{item.todo}}</h5>
            <span>
            <button v-on:click="editTodo(item.id)" class="btn btn-primary mr-3">Edit</button>
            <button v-on:click="removeTodo(item.id)" class="btn btn-danger">Delete</button>
            </span>
            </div>
          </div>
            
        </div>
        </div>
    </div>
</template>
<script>
export default {
  name: "todo",
  data() {
    return {
      todo: "",
      editing: false,
      list: [],
    };
  },
  methods: {
    //   add todo
    addTodo() {
      if (this.todo == "") {
        alert("please fill the field");
      } else {
        const newTodo = {
          id: new Date().getTime().toString(),
          todo: this.todo,
        };
        this.list.push(newTodo);
        this.todo = "";
      }
    },
    // remove todo
    removeTodo(id) {
      const newTodo = this.list.filter((item) => item.id !== id);
      this.list = newTodo;
      this.editing = false;
    },

    // edit todo

    editTodo(id) {
      this.editing = true;
      const newTodo = this.list.filter((item) => item.id == id);
      console.log(newTodo);
      this.todo = newTodo[0].todo;
    },
    updateTodo() {
      this.list[0].todo = this.todo;
      this.todo = "";
      this.editing = false;
    },
  },
};
</script>
<style lang="">
</style>