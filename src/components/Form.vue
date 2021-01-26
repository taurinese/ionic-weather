<template>
    <div class="ion-padding">
        <ion-item>
            <ion-input v-model="city" autofocus clear-input @keyup.enter="sendCity" color="primary"></ion-input>
        </ion-item>
    </div>
</template>

<script>
import { IonInput, IonItem } from '@ionic/vue';

export default ({
  components: { 
      IonInput, 
      IonItem 
    },
    name: "Form",
    data(){
        return {
            city: ""
        }
    },
    methods: {
        sendCity(){
            this.$emit('sent', this.city);
            this.city = ""
        }
    },
});
</script>

<style scoped>

</style>