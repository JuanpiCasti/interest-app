<template>
  <ion-page>
    <ion-tabs>
      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="calculadora" href="/tabs/calculadora">
          <ion-icon :icon="calculator" />
        </ion-tab-button>
          
        <ion-tab-button tab="tab2" href="/tabs/historial">
          <ion-icon :icon="timeOutline" />
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script lang="ts">
import { IonTabBar, IonTabButton, IonTabs, IonIcon, IonPage } from '@ionic/vue';
import { ellipse, square, triangle, calculator, timeOutline } from 'ionicons/icons';

export default {
  name: 'Tabs',
  components: {  IonTabs, IonTabBar, IonTabButton, IonIcon, IonPage },
  setup() {
    return {
      ellipse, 
      square, 
      triangle,
      calculator,
      timeOutline
    }
  }
}
</script>