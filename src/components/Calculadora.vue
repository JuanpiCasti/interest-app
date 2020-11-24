<template>
  <div id="container">
    <ion-card>
      <ion-card-header>
        <ion-card-subtitle>TEA: {{tea}}%</ion-card-subtitle>
        <ion-card-title>${{capitalFinal}}</ion-card-title>
      </ion-card-header>
    </ion-card>
    <ion-grid class="form">
      <ion-row class="form-module">
          <h3 class="form-title">Capital Inicial $</h3>
          <input type="number" class="form-input" v-model="capitalInicial">
      </ion-row>
      <ion-row class="form-module">
          <h3 class="form-title">Tasa Nominal Anual %</h3>
          <input type="number" class="form-input" v-model="tnaInput">
      </ion-row>
      <ion-row class="form-module">
          <h3 class="form-title">Tiempo en Meses</h3>
          <input type="number" class="form-input" v-model="tiempo">
      </ion-row>
      <ion-row class="form-module">
          <h3 class="form-title">Nombre</h3>
          <input type="text" class="form-input" v-model="nombre">
      </ion-row>
      <ion-row class="form-module">
          <h3 class="form-title">Tipo</h3>
          <select name="tipo" class="form-select" v-model="tipo">
            <option value="Crédito">Crédito</option>
            <option value="Inversión">Inversión</option>
          </select>
      </ion-row>
    </ion-grid>
    <ion-button color="primary" @click="test()">
      Guardar en Historial
    </ion-button>

      <ion-alert
      :is-open="isOpenRef"
      message="Por favor, complete todos los campos"
      :buttons="['ok']"
      @onDidDismiss="setClosed()"
      class="alerta"
      >
      </ion-alert>
  </div>


</template>

<script lang="js">
import { IonAlert, IonButton, ionCard, ionCardHeader, ionCardSubtitle, ionCardTitle, ionGrid, ionRow }   from '@ionic/vue';     
import { defineComponent, ref } from 'vue';

export default {
  name: 'Calculadora',
  components: { IonAlert, IonButton, ionCard, ionCardHeader, ionCardSubtitle, ionCardTitle, ionGrid, ionRow },
  props: {
    name: String,
  },
  data () {
    return {
        nombre: "",
        capitalInicial: "",
        tnaInput: "",
        tiempo: "",
        tipo:"",
        fecha: new Date(),
        isOpenRef: false,
        history: [],
    }
  },
  methods: {
    test() {    
      this.saveEntry()
    },

    updateLocalStorage() {
      this.history = JSON.parse(localStorage.getItem("history"));
    },

    saveEntry() {
      if (this.nombre && this.tipo != "" && this.capitalInicial && this.tiempo && this.tna) {
        const entry = {
          nombre: this.nombre,
          tipo: this.tipo,
          capitalInicial: this.capitalInicial,
          tna: this.tna,
          tea: this.tea,
          tiempo: this.tiempo,
          capitalFinal: this.capitalFinal,
          fecha: this.fechaParsed
        }
        this.history.unshift(entry);
        localStorage.setItem("history", JSON.stringify(this.history))
        console.log(this.history);
        this.nombre= "";
        this.capitalInicial= "";
        this.tnaInput= "";
        this.tiempo= "";
        this.tipo="";
        this.fecha= new Date();

      } else {
        this.isOpenRef = true;
      }
    },
    setClosed() {
      this.isOpenRef = false;
    }
  },
  computed: {
    tna() {
      return this.tnaInput
    },
    tasa() {
      return ((this.tna/100)/12)+1
    },
    tasaElevada() {
      return (this.tasa)**this.tiempo
    },
    capitalFinal() {
      return (this.capitalInicial*this.tasaElevada).toFixed(2)
    },
    tea() {
      return (((this.tasa**12)-1)*100).toFixed(2)
    },
    fechaParsed() {
      return `${this.fecha.getDate()}/${this.fecha.getMonth()}/${this.fecha.getFullYear()}`
    },
  },
  created() {
    setInterval(this.updateLocalStorage, 20);
    localStorage.setItem("history", history)
  }

}
</script>

<style scoped>
.icon-header {
  height: 5rem;
}

h1 {
  margin-top: 0rem;
}

ion-card {
  background-color: var(--ion-color-primary);
  border-radius: 1rem;
  border: solid black 1px;
  box-shadow: none;
  min-width: 80%;
  max-width: 100%;
}

ion-card-subtitle {
  position: absolute;
  top: 10%;
  color: #fff;
}

ion-card-title {
  font-size: 2rem;
  color: #fff;
}

ion-button {
  margin-top: 1.2rem;
  color: #fff;
  text-transform: none;
  width: 90%;
  font-size: 1.2rem;
  border-radius: 10px;
  border: solid 1px black;
  box-shadow: none;
}

ion-alert {
  color: black,
}

.alerta {
  padding: 0;
  color: black;
}

.icon-header {
  height: 3rem;
}

#container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 55%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  color: #8c8c8c;
  margin: 0;
}

#container a {
  text-decoration: none;
}



.form .form-module {
  margin: 0 auto;
  width: 90%;
  align-items: center;
  justify-content: space-between;
  flex-wrap: nowrap;
}

.form .form-module .form-title {
  font-size: 1.2rem;
}

.form-input {
  border: solid black 1px;
  border-radius: 5px;
}

.form-select {
  border: solid black 1px;
  border-radius: 5px;
}

.form .form-module:nth-child(1) .form-input {
  max-width: 45%;
}

.form .form-module:nth-child(2) .form-input {
  max-width: 20%;
}

.form .form-module:nth-child(3) .form-input {
  max-width: 20%;
}

.form .form-module:nth-child(4) .form-input {
  max-width: 65%;
}

</style>