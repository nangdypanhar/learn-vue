<!-- Option API -->

<!-- <script>
export default {
  data() {
    return {
      name: "Nangdy Panhar",
      status: "active",
      tasks: ["Task 1", "Task 2", "Task 3"],
      link: "https://dypanhar.me/",
    };
  },
  methods: {
    toggleStatus() {
      if (this.status == "active") {
        this.status = "pending";
      } else if (this.status == "pending") {
        this.status = "active";
      } else {
        this.status = "Unknown Status";
      }
    },
  },
};
</script> -->

<!-- Composition API  STYLE 1-->
<!-- <script>
import { ref } from "vue";

export default {
  setup() {
    const name = ref("Nangdy Panhar");
    const status = ref("active");

    const toggleStatus = () => {
      status.value = status.value === "active" ? "pending" : "active";
    };

    return { name, status, toggleStatus };
  },
};
</script> -->

<!-- Composition API  STYLE 2-->
<!-- 
<script setup>
import { ref } from "vue";

const name = ref("Nangdy Panhar");
const status = ref("active");

const toggleStatus = () => {
  status.value = status.value === "active" ? "pending" : "active";
};
</script>

<template>
  <h1>Tasks:</h1>
  <h1>{{ name }}</h1>
  <p>{{ status }}</p>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>

  <a :href="link">Click here for porfilio</a>

  <button v-on:click="toggleStatus">Change Status</button>
</template> -->

<script setup>
import { ref, onMounted } from "vue";

const tasks = ref(["Task1", "Task2", "Task3"]);
const newTask = ref("");
const editIndex = ref(null);
const editValue = ref("");

const addNewTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

const editTask = (index) => {
  editIndex.value = index;
  editValue.value = tasks.value[index];
};

const updatedTask = (index) => {
  tasks.value[index] = editValue.value;
  editIndex.value = null;
};

const cancledEdit = () => {
  editIndex.value = null;
};

onMounted(async () => {
  try {
    const response = await fetch(
      "https://api.jsoning.com/mock/hxknkkcuxg/tasks"
    );
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (err) {
    console.log("Error fetching");
  }
});
</script>

<template>
  <h1>Hello World</h1>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span v-if="editIndex == index">
        <form @submit.prevent>
          <input type="text" v-model="editValue" />
          <button type="submit" @click="updatedTask(index)">Update</button>
          <button type="submit" @click="cancledEdit">Cancel</button>
        </form></span
      >

      <span v-else>
        <span>{{ task }}</span>
        <button @click="deleteTask(index)">X</button>
        <button @click="editTask(index)">Edit</button>
      </span>
    </li>
  </ul>

  <form @submit.prevent>
    <label for="newTask">New Task </label>
    <input type="text" name="newTask" v-model="newTask" />
    <button type="submit" @click="addNewTask">Add New Task</button>
  </form>
</template>


<!-- we use :

- defineProps : when we want to accept props from other component.
- computed : when we want it to run once and cache the result mostly use with reactive and ref state. It only change once the dependencies change. -->