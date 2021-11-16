<template>
  <header>
    <h1>
      <p>Todo List </p>
      <p>completed <span>{{countTask}}</span></p>
    </h1>
    <div>
      <h5>we advise you to always start with the most important spots.</h5>
      <template v-for="(priority, index) in priorities" :key="index">
        <div class="remember">{{index}} - {{priority}}</div>
      </template>
    </div>
    <form>
      <div class="form">
        <input type="text" placeholder="add new task" v-model="task">
        <button @click.prevent="addNewTask"><ion-icon name="arrow-forward-outline"></ion-icon></button>
      </div>
    </form>
  </header>

  <main>
    <div v-for="(task, index) in tasks" :key="index" class="footer">
      <p @click="deleteTask(index)"><span>not longer to see</span> <span>x</span></p>
      <p><span>{{task.name}}</span> <span> added {{`${manageTime().day} ${manageTime().date} ${manageTime().month} ${manageTime().year}`}} at {{`${manageTime().hour} ${manageTime().minute}`}}</span></p>
      <p><input type="checkbox"  @click="getPriority(index)">yes i must have priority over the other tasks</p>
    </div>
  </main>
</template>


<script>
import {reactive, computed, ref} from 'vue'
export default {
  name: 'App',
  setup(){
    const tasks = reactive([]);
    const task = ref('')
    const isChecked = ref(false)
    const priorities = reactive([])
    const countTask = computed(() => tasks.length)
    const addNewTask = () => {
      const haveBeenAdded = tasks.some(item => item.name === task.value)
      if(task.value.length < 5){
        alert('proud valid task. not accept empty')
        console.log(task.value)
      }
      else if(haveBeenAdded === false){
        tasks.push({name: task.value, status: isChecked.value})
      }
      else{
        alert('this task already existed. make sure to enter newer')
      }
      task.value = ""
    }
    const getPriority = (index) => {
      if (tasks[index].status === false) {
        tasks[index].status = true
        priorities.push(tasks[index].name)
      } else if (tasks[index].status === true) {
        tasks[index].status = false
        priorities.splice(index, 1)
      }
    }
    const manageTime = () => {
      const daysOfWeek = ['Sun','Mon','Tue','Wed','Thu','Fri','Sat']
      const months = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];

      return {
        day: daysOfWeek[new Date().getDay()],
        date: new Date().getDate(),
        month: months[new Date().getMonth()-1],
        year: new Date().getFullYear(),
        hour: new Date().getHours(),
        minute: new Date().getMinutes()
      }
    }
    const deleteTask = (index) => {
      tasks.splice(index, 1)
      priorities.splice(index, 1)
    }
    return{
      tasks, task, countTask, priorities,
      addNewTask, manageTime, getPriority, deleteTask
    }
  }
}
</script>

<style>
header{
  display: flex;
  flex-direction: column;
}
header h1{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  font-size: 18px;
  box-shadow: 0px 2px 0px #ccc;
  padding-bottom: 15px;
}
header h1 p span{
  background-color: rgb(133, 116, 116);
  color: #fff;
  padding: 5px 10px;
  border-radius: 4px;
  font-size: 18px;
}
h5{
  font-size: 15px;
  text-align: center;
}
.remember{
  padding: 10px;
  text-align: center;
  font-size: 16px;
  border: 1px solid #fff;
  box-shadow: 0px 0px 5px #4b7270;
  margin-left: 70px;
  margin-right: 70px;
}
form{
  margin-left: -1%;
  margin-right: -1%;
  padding: 20px 30px;
  background-color: #ccc;
  margin-top: 50px;
}
.form{
  display: flex;
  border: 1px solid #fff;
  padding: 5px 10px;
  position: relative;
  width: 90%;
  height: 30px;
  margin: 50px auto;
  background-color: #fff;
}
.form input{
  border: none;
  background: none;
  outline: none;
  width: 91%;
}
.form button{
  position: absolute;
  right: 0;
  top: 0;
  height: 100%;
  line-height: 45px;
  padding-right: 15px;
  padding-left: 15px;
  color: #fff;
  background-color:rgb(133, 116, 116);
  font-weight: bolder;
  font-size: 16px;
  border: none;
}
</style>
