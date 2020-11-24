<template>
  <div id="container">
    <ion-grid class="history-list">
      <ion-row 
        v-for="(entry, index) in history"
        :key="index">
        <div class="card">
          <div>
          <span class="card-title">{{entry.nombre}}</span>
          <span class="card-subtitle">{{entry.tipo}}</span><br/>
          <span class="card-ci">CI: ${{entry.capitalInicial}}</span>
          <span class="card-TEA">TEA: {{entry.tea}}%</span>
          <span class="card-TNA">TNA: {{entry.tna}}%</span><br/>
          <span class="card-Tiempo">Tiempo: {{entry.tiempo}} <span v-if="entry.tiempo==1">Mes</span><span v-if="entry.tiempo > 1">Meses</span></span>
          <span class="card-CF">CF: ${{entry.capitalFinal}}</span><br/>
          <span class="card-time">Fecha: {{entry.fecha}}</span>
          <button class="card-delete" @click="deletear"><ion-icon :icon="trashOutline"/></button>
          </div>
        </div>
      </ion-row>
      <div class="no-elements" v-if="empty">
        <p>Aún no hay elementos guardados.</p>
      </div>
    </ion-grid>
  </div>
</template>

<script lang="js">
import { ionGrid, ionRow }   from '@ionic/vue';     
import { trashOutline } from 'ionicons/icons';

export default {
  name: 'Historial',
  components: {ionGrid, ionRow},
  setup() {
    return {
      trashOutline
    }
  },
  props: {
    name: String
  },
  data() {
    return {
      history: [],
      empty: true,
      modoDelete: false,
    }
  },
  methods: {
    updateLocalStorage() {
      this.history = JSON.parse(localStorage.getItem("history"));
      console.log(this.history)
      if (this.history == false) {
        this.empty = true;
      } else {
        this.empty = false;
      }
    },
    deletear(index) {
      this.history.splice(index, 1),
      localStorage.setItem("history", JSON.stringify(this.history));
    },
    setClosed() {
      this.modoDelete = false;
    }
  },
  created() {
    setInterval(this.updateLocalStorage, 20);
  },
  
}
</script>

<style scoped>
  .no-elements {
    text-align: center;
  }

  .history-list {
    margin-top: 10rem;
  }

  ion-row {
    justify-content: center;
  }

  .card {
    width: 90%;
    box-shadow: none;
    border: solid black 1px;
    border-radius: 10px;
    padding: .2rem;
    text-align: center;
    font-size: .8rem;
    position: relative;
    margin-bottom: 1rem;
  }

  .card .card-title {
    font-size: 1.5rem;
  }

  .card .card-subtitle {
    font-size: 1rem;
    margin-left: .8rem;
    color: #b3b3b3;
  }

    .card .card-TEA, .card .card-TNA {
      margin-left: .6rem;
  }

    .card .card-CF {
      margin-left: .6rem;
    }
  .card .card-delete {
    background-color: #fff;
    position: absolute;
    right: 1rem;
    bottom: 0;
  }

  .card .card-delete ion-icon {
    color: #eb445a;
  }
</style>