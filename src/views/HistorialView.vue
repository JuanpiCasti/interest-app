<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Historial</ion-title>
        </ion-toolbar>
      </ion-header>
      <Historial/>
      <HeaderHistorial/>

    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import HeaderHistorial from "@/components/HeaderHistorial.vue"
import Historial from "@/components/Historial.vue"

export default  {
  name: 'Tab2',
  components: { HeaderHistorial, Historial, IonHeader, IonToolbar, IonTitle, IonContent, IonPage }
}
</script>