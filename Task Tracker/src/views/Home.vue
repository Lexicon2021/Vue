<template>
    <AddTask v-show="showAddTask" @add-task="AddTask" />
  <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask"  :tasks="tasks"/>
</template>

<script>

import Tasks from '../components/Tasks.vue';
import AddTask from '../components/AddTask.vue';


export default {
    name: 'Home',
    props: {
        showAddTask: Boolean,
    },
    components: {
        Tasks,
        AddTask
    },

    data() {
        return {
            tasks: []
        }
    },
    methods: {
    async AddTask(task) {

      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(task)
      });

      const data = await res.json();




      this.tasks = [...this.tasks, data];
    },
    async deleteTask(id) {
      if(confirm('Do you want to delete task?')) {

        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        });

        res.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert('Error deleting task');



        
      }
    },
    async toggleReminder(id) {


      const taskToToggle = await this.fetchTask(id);
      const updateTask = {...taskToToggle, reminder: !taskToToggle.reminder};

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updateTask)
      });

      const data = await res.json();


      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data .reminder} : task)
    },
    async fetchTasks() {
      const res = await fetch('api/tasks');

      const data = await res.json();

      return data;
    },
    async fetchTask(id) { //*** fetch individual task */
      const res = await fetch(`api/tasks/${id}`); // http://localhost:5000

      const data = await res.json();

      return data;
    },
    // async fetchTasks() { //*** after proxy */
    //   const res = await fetch('http://localhost:5000/tasks');

    //   const data = await res.json();

    //   return data;
    // },
    // async fetchTask(id) { //*** fetch individual task */
    //   const res = await fetch(`http://localhost:5000/tasks/${id}`);

    //   const data = await res.json();

    //   return data;
    // }
  },
  async created() {
    // this.tasks = [
    //   {
    //     id: 1,
    //     text: 'Doctors Appointment',
    //     day: 'March 1st at 2:30pm',
    //     reminder: true
    //   },
    //   {
    //     id: 2,
    //     text: 'Meeting at School',
    //     day: 'March 3rd at 1:30pm',
    //     reminder: 'true'
    //   },
    //   {
    //     id: 3,
    //     text: 'Food Shopping',
    //     day: 'March 3rd at 11:am',
    //     reminder: false
    //   }
    // ]

    this.tasks = await this.fetchTasks();
  }
}
</script>