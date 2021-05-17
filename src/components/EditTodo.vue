<template>
  <div class="edit__todo">
    <b>Edit Task</b>
    <!-- Edit task space-->

    <!-- Edit task input -->
    <input
      :placeholder="taskDataEdit.description"
      v-model="editTask"
      type="text"
    />
    <!-- Edit task button group (Edit, Close) -->
    <div class="edit__todo__buttons">
      <button @click="changeTask()" type="submit" class="submit">Submit</button>
      <button @click="closeEditTask()" class="close">Close</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["taskDataEdit"],
  data() {
    return {
      editTask: "",
    };
  },
  methods: {
    // Change task description when complete edit task action
    changeTask: function () {
      this.taskDataEdit.description = this.editTask;
      this.taskDataEdit.isEditting = false;
      this.editTask = "";
    },

    // Stop edit task action
    closeEditTask: function () {
      this.taskDataEdit.isEditting = false;
      this.editTask = "";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.edit__todo {
  padding-top: 16px;
  width: 50%;
  b {
    display: block;
    margin-bottom: 16px;
    color: rgb(15, 23, 124);
    font-size: 24px;
  }
  // Style input text
  input[type="text"],
  select {
    width: 100%;
    padding: 12px 20px;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
    margin-right: 50px;
    margin-bottom: 20px;
    &:focus-visible {
      outline: none;
    }
  }

  // Define button
  button {
    height: 41px;
    color: #fff;
    border-radius: 10px;
    &:hover {
      opacity: 0.8;
      cursor: pointer;
    }
  }

  // Possition button group
  .edit__todo__buttons {
    // Style submit button
    .submit {
      background-color: rgb(15, 23, 124);
      margin-right: 10px;
    }

    //Style close button
    .close {
      background-color: rgb(141, 12, 12);
    }
  }
}
</style>
