<template>
  <div id="app">
    <div class="container">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
  <a class="navbar-brand" href="#">tuboltseva</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="navbarNavDropdown">
    <ul class="navbar-nav">
      <li class="nav-item active">
        <a class="nav-link" href="pro.vue"> Каталог процессоров <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Каталог материнских плат</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#"> Главная </a>
      </li>
    </ul>
  </div>
</nav>

<!-- основа -->
<br>
<h1> Каталог материнских плат </h1>
<br>

<div class="form-group">
  <label for=""> Название материнской платы </label>
  <input type="text" class="form-control" v-model="name" />
</div>

<div class="form-group">
  <label for=""> Цена </label>
  <input type="text" class="form-control" v-model="sum" />
</div>

<button class="btn btn-primary" @click="onSave"> Добавить </button>
<br>

<div class="row" v-for="note in mate" :key="note.id">
  <div class="col-4"> {{note.name}} </div>
  <div class="col-4"> {{note.sum}}</div>
  <div class="col-4"> <button class="btn btn-danger" @click="onDelete(note.id)"> Удалить </button></div>
</div>
<br>

<!-- Процессоры -->
<br>
<h1> Каталог процессоров </h1>
<br>

<div class="form-group">
  <label for=""> Название процессора </label>
  <input type="text" class="form-control" v-model="model" />
</div>

<div class="form-group">
  <label for=""> Цена </label>
  <input type="text" class="form-control" v-model="price" />
</div>

<button class="btn btn-primary" @click="onSaveOne"> Добавить </button>
<br>


<div class="row" v-for="note in process" :key="note.id">
  <div class="col-4"> {{note.model}} </div>
  <div class="col-4"> {{note.price}}</div>
  <div class="col-4"> <button class="btn btn-danger" @click="onDeleteOne(note.id)"> Удалить </button></div>
</div>
<br>



<!-- футер -->
  <div class="row" style="background-color: gray">
    <div class="col-sm-4"> 
      Тубольцева Анастасия Сергеевна 
      <br>
      группа: 181-362 
      </div>

    <div class="col-sm-4"> Дата выполнения: 
      <br>
      17.06.2020 
      </div>

    <div class="col-sm-4"> Документация
      <br>
      <a href="https://developer.mozilla.org/ru/" target="_blank"> MDN </a>
    </div>

  </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return{
      mate: [],
      name: '',
      sum: '',
      process: [],
      model: '',
      price: ''
    };
  },
  components: {},
  methods: {
    async updateData() {
      try{
        let res = await this.$http.get("http://localhost:3000/mate");
        this.mate = await res.json();
      } catch(err) {
        console.error(err);
      }
    },
    async onSave() {
      let note = {
        name: this.name,
        sum: this.sum
      };
      try {
        await this.$http.post("http://localhost:3000/mate", note);
        this.updateData();
      } catch(err) {
        console.error(err);
      }
    },
     async onDelete(id) {
      try{
        await this.$http.delete("http://localhost:3000/mate/" + id);
        this.updateData();
      } catch(err) {
        console.error(err);
      }
    },
    async updateDataOne() {
      try{
        let res = await this.$http.get("http://localhost:3000/process");
        this.process = await res.json();
      } catch(err) {
        console.error(err);
      }
    },
    async onSaveOne() {
      let note = {
        model: this.model,
        price: this.price
      };
      try {
        await this.$http.post("http://localhost:3000/process", note);
        this.updateDataOne();
      } catch(err) {
        console.error(err);
      }
    },
     async onDeleteOne(id) {
      try{
        await this.$http.delete("http://localhost:3000/process/" + id);
        this.updateDataOne();
      } catch(err) {
        console.error(err);
      }
    }
  },
  created() {
    this.updateData();
    this.updateDataOne();
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: cornflowerblue;
}
</style>
