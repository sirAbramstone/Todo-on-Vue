<template>
  <div>
    <input 
    type="text" 
    name="" 
    id="" 
    @keyup.enter="addTask"
    v-model="currentTask"
    >
    <ul>
      <li
      v-for="task in tasks"
      :key="task.id"
      :class="{'strike': task.isCompleted}"
      >
        <input
         type="text"
         v-if="task.isEditing"
         @keyup.enter="editTask(task.text)"
         v-model="editValue"
         >
        <span
          v-else
          @click="task.isCompleted = !task.isCompleted"
        >{{task.text}}</span>
        <button @click="removeTask(task.text)">X</button>
        <button @click="changeEditing(task.text)">*</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      currentTask: '',
      editValue: '',
      tasks: [
        {
          text: "Доделать сайт",
          isCompleted: false,
          isEditing: false
        },
        {
          text: "Выучить Вуй",
          isCompleted: false,
          isEditing: false
        },
        {
          text: "Доделать тудушечку",
          isCompleted: true,
          isEditing: false
        }
      ]
    };
  },
  methods: {
    addTask: function () {
      this.tasks.push({
        text: this.currentTask,
        isCompleted: false
      });
      this.currentTask = '';
    },
    removeTask: function (taskText) {
      this.tasks = this.tasks.filter(task => {
        return task.text !== taskText;
      })
    },
    changeEditing: function(taskText) {
      this.editValue = taskText;
      this.tasks = this.tasks.map(task => {
        if (task.text === taskText) {
          task.isEditing = !task.isEditing;
        }
        return task;
      })
    },
    editTask: function(taskText) {
      this.tasks = this.tasks.map(task => {
        if (task.text === taskText) {
          task.isEditing = !task.isEditing;
          task.text = this.editValue;
        }
        return task;
      })
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  cursor: pointer;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.strike {
  text-decoration: line-through;
}
</style>
