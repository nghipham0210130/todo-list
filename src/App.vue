<template>
  <div id="app">
    <!-- Header -->
    <header>
      <div class="container">
        <span>{{ appName }}</span>
        <ul>
          <li><a>Home</a></li>
          <li><a>Todo List</a></li>
        </ul>
      </div>
    </header>
    <!-- Main -->
    <main class="container">
      <!-- Notification add task action successq (lasts for 5 seconds since add action success) -->
      <div v-show="isAddSuccess" class="add__task--success">
        <p><b>Success!</b> Entity created</p>
      </div>
        <!-- Search -->
        <div class="search">
          <input
            name="search"
            class="form-control"
            type="text"
            v-model="searchQuery"
            placeholder="Search"
          />
        </div>
        <!-- Add task -->
        <div class="add__task">
          <input
            type="text"
            v-model="newTask"
            v-on:keyup.enter="addTask()"
            placeholder="Enter new task . . ."
          />
          <button @click="addTask()">Add</button>
        </div>
        <!-- Display each element from resultQuery -->
        <home
          @delete="deleteTask"
          v-for="(task, index) in resultQuery"
          :key="index"
          :taskData="task"
        />
    </main>
  </div>
</template>

<script>
import Home from "./components/Home.vue";

export default {
  name: "App",
  components: {
    home: Home,
  },
  data() {
    return {
      appName: "Todo List",
      newTask: "",
      isAddSuccess: false,
      searchQuery: "",
      tasks: [
        { id: 0, description: "Item1", isDone: false, isEditting: false },
        { id: 1, description: "Item2", isDone: true, isEditting: false },
        { id: 2, description: "Item3", isDone: false, isEditting: false },
        { id: 3, description: "Item4", isDone: true, isEditting: false },
      ],
    };
  },
  computed: {
    // filter task when enter on this.searchQuery exist
    resultQuery() {
      if (this.searchQuery != "") {
        return this.tasks.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => {
              return item.description.toLowerCase().includes(v);
            });
        });
      } else {
        return this.tasks;
      }
    },
  },
  methods: {
    // Add new task
    addTask() {
      if (this.newTask !== "") {
        // get position last element of array
        const lastId = this.tasks.length;
        if (lastId === 0) {
          this.tasks.push({
            // set id of new task by id of last element of array plus 1
            id: 0,
            description: this.newTask,
            isDone: false,
            isEditting: false,
          });
        } else {
          this.tasks.push({
            // set id of new task by id of last element of array plus 1
            id: this.tasks[lastId - 1].id + 1,
            description: this.newTask,
            isDone: false,
            isEditting: false,
          });
        }

        (this.newTask = ""),
          (this.isAddSuccess = true),
          // Hidden notification add task action success after 5s
          setInterval(() => (this.isAddSuccess = false), 5000);
      }
    },
    // Delete task with value = id invited from delete action on Home
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
  },
};
</script>

<style lang="scss" >
// Style container
.container {
  max-width: 1170px;
  padding-left: 15px;
  padding-right: 15px;
  margin: 0 auto;
}
// Style div tag common
div {
  border-radius: 10px;
}
// Style header
header {
  background-color: rgba(22, 22, 24, 0.603);
  height: 80px;
  margin-bottom: 80px;
  // Style container
  .container {
    color: #fff;
    max-width: 1170px;
    height: 70px;
    padding-left: 15px;
    padding-right: 15px;
    margin: 0 auto;
    font-size: 24px;
    font-weight: 600;
    // Style ul in header
    ul {
      list-style-type: none;
      display: inline-block;
      font-size: 18px;
      // Arranged horizontally
      li {
        display: inline;
        line-height: 32px;
        list-style: none;
        text-align: center;
        // Style a tag
        a {
          color: #fff;
          padding: 24px 20px 36px 18px;
          transition: all 0.2s ease-in-out;
          text-decoration: none;
          &:hover {
            opacity: 0.5;
            transform: scale(1.5);
            cursor: pointer;
            background-color: rgba(22, 22, 24, 0.61);
            font-size: 15px;
            padding-top: 27px;
          }
        }
      }
    }
  }
}
// Style main
main {
  // Style otification add task action success
  .add__task--success {
    border: 1px solid rgba(132, 228, 132, 0.288);
    background-color: rgba(120, 216, 120, 0.521);
    border-radius: 10px;
    margin-bottom: 30px;
    p {
      width: 100%;
      color: rgb(15, 70, 15);
      margin: 30px 20px 20px 20px;
      font-size: 18px;
      b {
        font-weight: 900;
      }
    }
  }
  // Style search
  .search {
    margin-bottom: 15px;
    width: 30%;
    float: right;
    input[type="text"],
    select {
      width: 100%;
      padding: 12px 20px;
      display: inline-block;
      border: 1px solid rgb(49, 47, 47);
      border-radius: 10px;
      box-sizing: border-box;
      &:focus-visible {
        outline: none;
      }
    }
  }
  // Style addTask
  .add__task {
    margin-bottom: 30px;
    // Style input
    input[type="text"],
    select {
      width: 90%;
      padding: 12px 20px;
      display: inline-block;
      border: 1px solid #ccc;
      border-radius: 4px 0 0 4px;
      box-sizing: border-box;
      &:focus-visible {
        outline: none;
      }
    }
    // Style button add task
    button {
      float: right;
      height: 41px;
      width: 10%;
      background-color: rgba(10, 10, 87, 0.877);
      color: #fff;
      border-radius: 0 10px 10px 0;
      &:hover {
        opacity: 0.8;
        cursor: pointer;
      }
    }
  }
}
</style>
