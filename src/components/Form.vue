<template>
  <button @click="toggleModal">Add Task</button>
  <div>
    <table>
      <thead>
        <tr>
          <th>Check</th>
          <th>Task</th>
          <th>Priority</th>
          <th>Date</th>
          <th>Time</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in todoTasks" :key='index'>
          <td  v-if="showIcons"> 
            <input v-if="task.title" type="checkbox">
          </td>
          <td>{{task.title}}</td>
          <td>{{task.priorityLevel}}</td>
          <td>{{task.deadline}}</td>
          <td>{{task.timeDeadline}}</td>
          <td>
            <span v-if="showIcons" class="icon">
              <i v-if="task.title" @click="editTask(index)" class="ri-edit-2-fill"></i>
              <i v-if="task.title" @click="deleteTask(index)" class="ri-delete-bin-5-line"></i>
            </span>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
  
  <form v-if="showModal">
    <div class="backdrop">
      <div class="modal">
        <button v-if="showModal" @click="toggleModal" class="cancel">X</button>
        <div>
          <p class="">To-Do Task</p>
          <label>Task:</label>
          <input type="text" required v-model="text" placeholder="Enter your task">
        </div>
        <label>Priority</label>
        <select v-model="priority">
          <option value="5">High</option>
          <option value="3">Medium</option>
          <option value="1">Low</option>
        </select>
        <label for="date">Date</label>
        <input type="date" v-model="date" required>
        <label for="time">Time</label>
        <input type="time" v-model="time" required>

        <button type="submit" @click.prevent="toggleSubmit" >Submit</button>
      </div>
    </div>
    <div>
      <button>completed Tasks</button>
    </div>
        
  </form>
</template>

<script>
export default {
  data() {
    return {
      text: '',
      priority: '',
      date: '',
      time: '',
      showModal: false,
      showIcons: false,
     
     todoTasks: [
        {
        title: '',
        priorityLevel: '',
        deadline: '',
        timeDeadline: '',
        }

      ]
    }
  },
  methods: {
    toggleSubmit(){
     if (this.text.length === 0 || this.priority == '' || this.date == '' || this.time == '') {
       alert('enter fields')
       return;
     };
    if(this.text.length > 0){
       this.showIcons = true;
     }
     {
       this.todoTasks.push({
         title: this.text,
         priorityLevel: this.priority,
         deadline: this.date,
         timeDeadline: this.time,
         });
      };
      
      this.text ='';
      this.priority ='';
      this.date ='';
      this.time ='';
      this.showModal = !this.showModal

    },

    toggleModal() {
      this.showModal = !this.showModal
    },
    deleteTask(index) {
      this.todoTasks.splice(index, 1);
    },
    
    editTask(index) {
      this.task = this.todoTasks[index].title;
      this.editedTask = index;
    },
    editTask() {
      this.showModal = !this.showModal
    }
  }
}
</script>

<style>
table {
  font-family: 'Open Sans', sans-serif;
  width: 750px;
  border-collapse: collapse;
  border: 3px solid #44475C;
  margin: auto;
  height: 100%;
}

table th {
  text-transform: uppercase;
  text-align: left;
  background: #44475C;
  color: #FFF;
  cursor: pointer;
  padding: 8px;
  min-width: 30px;
}
table th:hover {
  background: #717699;
}
table td {
  text-align: left;
  padding: 8px;
  border-right: 2px solid #7D82A8;
}
table td:last-child {
  border-right: none;
}
table tbody tr:nth-child(2n) td {
  background: #D4D8F9;
}
.modal {
  width: 400px;
  height: 500px;
  padding: 20px;
  margin: 50px auto;
  background-color: white;
  border-radius: 10px;
    
}
.backdrop {
  top: 0;
  position: fixed;
  background-color: rgba(0,0,0,0.5);
  width: 100%;
  height: 100%;
}
.cancel {
  background-color: crimson;
  margin: 0;
  padding: 5px 10px;
  border-radius: 0;
  display: flex;
  justify-content: right;

}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input, select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
} 
button {
  background-color: #1f61e7;
  border: 0;
  padding: 10px 20px;
  margin: 20px;
  color: white;
  border-radius: 20px;
    
}

@media screen and (max-width: 768px) {
  template {
    width: 100%;
    height: 100%;
  }
  table {
    overflow: auto;
    width: 100%;
  }

  .modal {
    width: 300px;
    margin: 0;
  }
}
</style>