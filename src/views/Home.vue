<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title class="ion-text-center">Ionic Weather</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content>
<!--       <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large" class="ion-text-center">App</ion-title>
        </ion-toolbar>
      </ion-header> -->
    
      <div id="container">
          <Form @sent="getCity"></Form>
          <Display v-if="city" :city="city"></Display>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import Form from "@/components/Form.vue";
import Display from "@/components/Display.vue";

export default({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    Form,
    Display
  },
  data(){
    return {
      city: null
    }
  },
  methods: {
    getCity(data){
      this.city = data;
    }
  },
});
</script>

<style scoped>
#container {
  text-align: center;
  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
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
</style>