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


<template>
  <header>
    <h1>
      <p>Todo List </p>
      <p>completed <span>{{HowManytask}}</span></p>
    </h1>
    <div>
      <h5>we advise you to always start with the most important spots.</h5>
      <template v-for="task in tasks" :key="task.name">
        <div class="remember" v-if="task.check = true">{{task.name}}</div>
      </template>
    </div>
    <form>
      <div class="form">
        <input type="text" placeholder="add to list" v-model="todo">
        <button @click.prevent="addTodo"><ion-icon name="arrow-forward-outline"></ion-icon></button>
      </div>
    </form>
  </header>

  <main>
    <div v-for="task in tasks" :key="task.name" class="footer">
      <p><span>not longer to see</span> <span>x</span></p>
      <p><span>{{task.name}}</span> <span> added {{`${task.intime.indate.day} ${task.intime.indate.date} ${task.intime.indate.month} ${task.intime.indate.year}`}} at {{`${task.intime.time.hour} ${task.intime.time.minute}`}}</span></p>
      <p><input type="checkbox" v-model="check" @click="checking">yes i must have priority over the other tasks</p>
    </div>
  </main>
</template>


<script>
export default {
  name: 'App',
  data(){
    return{
      todo: '',
      check: false,
      tasks: []
    }
  },
  methods:{
    addTodo(){
      let days = ['Sun','Mon','Tue','Wed','Thu','Fri','Sat'],
          months = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
      return this.tasks.push(
        {
          name: this.todo,
          intime:{
            indate:{
              day: days[new Date().getDay()],
              date: new Date().getDate(),
              month: months[new Date().getMonth()-1],
              year: new Date().getFullYear()
            },
            time:{
              hour: new Date().getHours(),
              minute: new Date().getMinutes()
            }
          },
          checked: this.check
        }
      )
    }
  },
  computed:{
    HowManytask(){
      return this.tasks.length;
    }
  }
}
</script>

















