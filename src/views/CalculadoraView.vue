<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Calculadora</ion-title>
        </ion-toolbar>
      </ion-header>
      <HeaderCalculadora/>
      <Calculadora/>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import Calculadora from '@/components/Calculadora.vue';
import HeaderCalculadora from '@/components/HeaderCalculadora.vue';

export default  {
  name: 'Tab1',
  components: { HeaderCalculadora, Calculadora, IonHeader, IonToolbar, IonTitle, IonContent, IonPage }
}
</script>