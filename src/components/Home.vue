<template>
  <!-- Todo List -->
  <div class="home">
    <input type="checkbox" v-model="taskData.isDone" />
    <span :class="{ isDone: taskData.isDone }">{{ taskData.description }}</span>
    <div v-show="taskData.isEditting">
      <edit__todo :taskDataEdit="taskData"></edit__todo>
    </div>
    <!-- Button group directive Todo item (Delete, Edit) -->
    <div class="home__buttons">
      <button @click="deleteTask()" class="delete">Delete</button>
      <button @click="editTask(), (showModal = true)" class="edit">Edit</button>
    </div>
  </div>
</template>

<script>
import EditTodo from "./EditTodo.vue";

export default {
  components: {
    edit__todo: EditTodo,
  },
  props: ["taskData"],
  data() {
    return {
      showModal: false,
    };
  },
  methods: {
    // Transmission delete action with id of taskData to App.vue
    deleteTask: function () {
      console.log(this.taskData.id);
      this.$emit("delete", this.taskData.id);
    },
    // Change status isEditting to show edit-todo
    editTask: function () {
      this.taskData.isEditting = !this.taskData.isEditting;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.home {
  border: 1px solid #000;
  border-radius: 4px;
  padding: 40px 20px;
  display: block;
  position: relative;
  input {
    margin-right: 20px;
  }
  span {
    width: 100%;
    color: rgb(15, 70, 15);
    font-size: 18px;
  }
  .isDone {
    text-decoration: line-through;
  }
  button {
    height: 40px;
    color: #fff;

    &:hover {
      cursor: pointer;
      opacity: 0.8;
    }
  }
  .home__buttons {
    position: absolute;
    right: 20px;
    top: 32px;
    height: 25px;

    .delete {
      background-color: rgb(141, 12, 12);
      margin-right: 10px;
      padding: 10px 20px;
    }
    .edit {
      background-color: rgb(9, 148, 9);
      padding: 10px 20px;
    }
  }
}
</style>
