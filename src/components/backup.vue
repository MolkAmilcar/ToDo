<template>
  <header class="header">
    <h2>ToDoer</h2>
  </header>
  <div class="container main">
    <div class="d-flex">
      <input v-model="tarea" type="text" placeholder="Ingresa tarea" class="form-control mt-5">
      <button @click="submitTarea()" class="btn btn-warning button mt-5">+</button>
    </div>
    
    <ul class="list-group mt-4">
      <li @mouseover="hoverNC=true" @mouseleave="hoverNC=false"
      class="list-group-item" v-for="(tarea, index) in tareasNoCompletadas" :key="index">
      <span v-show="!hoverNC">{{ tarea.nombre }} </span>
      <div class="row" v-show="hoverNC">
      <div class="column">
        <img class="icon" v-show="hoverNC" src="../assets/tick.png" alt=""
        @click="completar(index)"></div>
      <div class="column">
        <img class="icon" v-show="hoverNC" src="../assets/cerrar.png" alt=""
        @click="eliminarNoCompletada(index)"></div>
      </div>
      </li>
    </ul>

    <ul class="list-group mt-4">
      <li class="list-group-item active" @click ="openList1()">Tareas completadas<img class="arrow-down" src="../assets/down-arrow.png" alt=""></li>
    </ul>
    <ul class="list-group " id="listaCompletados" style="display: none">
      <li @mouseover="hoverC=true" @mouseleave="hoverC=false"
      class="list-group-item" v-for="(tarea, index) in tareasCompletadas" :key="index">
      <span v-show="!hoverC">{{ tarea.nombre }} </span>
      <div class="row" v-show="hoverC">
      <div class="column">
        <img class="icon" v-show="hoverC" src="../assets/upload.png" alt=""
        @click="descompletar(index)"></div>
      <div class="column">
        <img class="icon" v-show="hoverC" src="../assets/cerrar.png" alt=""
        @click="eliminarCompletada(index)"></div>
      </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      tarea: "",
      tareasNoCompletadas: [
        {
          nombre: "Tarea no completada 1",
        },
        {
          nombre: "Tarea no completada 2",
        },
      ],
      tareasCompletadas: [
        {
          nombre: "Tarea completada 1",
        },
        {
          nombre: "Tarea completada 2",
        }
      ],
      hoverNC: false,
      hoverC: false,
    }
  },
  methods: {
    submitTarea() {
      if (this.tarea.length === 0) return;
      this.tareasNoCompletadas.push({
        nombre: this.tarea
      })
      this.tarea = "";
    },
    openList1() {
    var list = document.getElementById("listaCompletados");

    if (list.style.display == "none"){
        list.style.display = "block";
    }else{
        list.style.display = "none";
    }
  },
  eliminarNoCompletada(index){
    this.tareasNoCompletadas.splice(index, 1);
  },
  eliminarCompletada(index){
    this.tareasCompletadas.splice(index, 1)
  },
  completar(index){
    this.tareasCompletadas.push({
      nombre: this.tareasNoCompletadas[index].nombre
    })
    this.eliminarNoCompletada(index)
  },
  descompletar(index){
    this.tareasNoCompletadas.push({
      nombre: this.tareasCompletadas[index].nombre
    })
    this.eliminarCompletada(index)
  }
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  background-color: teal;
  padding: 10px;
  color: aliceblue;
}

.button {
  border-radius: 100%;
  color: aliceblue;
}

.table-color {
  background-color: aliceblue;
}

.icon {
  height: 15px;
  width: auto;
}

.arrow-down{
  height: 20px;
  width: auto;
  margin-left: 4px;
}
.tareas-completadas{
  color: aliceblue;
  background-color: teal;
  border-radius: 2px;
  padding-top: 4px;
  padding-left: 10px;
}
.column{
  float: left;
  width: 50%;
  text-align: center;
}
.row:after {
  content: "";
  display: table;
  clear: both;
}

</style>
