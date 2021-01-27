<template>
    <div v-if="weather.weather">
            <ion-card class="ion-padding" color="tertiary">
                <ion-card-title> {{ weather.name}} </ion-card-title>
                <ion-card-subtitle> 
                    <ion-row class="ion-align-items-center ion-justify-content-center">
                        <span>{{ capitalize(weather.weather[0].description) }}</span> <img :src="`http://openweathermap.org/img/w/${ weather.weather[0].icon }.png`"> 
                    </ion-row>
                    </ion-card-subtitle>
                <ion-card-content>
                    <i class="fas fa-thermometer-half"></i> {{ weather.main.temp }}°C | <i class="fas fa-wind"></i> {{ parseInt(weather.wind.speed) *3.6 }} km/h | <i class="fas fa-tint"></i> {{ weather.main.humidity }}%
                </ion-card-content>
            </ion-card>
    </div>
</template>

<script>
import { IonCard, IonCardContent, IonCardTitle, IonCardSubtitle, toastController, IonRow } from '@ionic/vue';
    export default({
        name: "Display",
        components: { IonCard, IonCardContent, IonCardTitle, IonCardSubtitle, IonRow },        
        data(){
            return {
                weather: {},
                error: false
            }
        },
        mounted(){
            this.fetchWeather()
        },
        props: ['city'],
        methods: {
            fetchWeather(){
                fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${process.env.VUE_APP_API_KEY}&units=metric&lang=fr`)
                .then(res => res.json())
                .then(json => {
                    console.log(json)
                    this.weather = "";
                    this.error = "";
                    if(json.cod == 404) {
                        this.error = json;
                        this.openToast(this.capitalize(json.message));
                    }
                    else this.weather = json;
                })
                
            },
            capitalize(text){
                return text[0].toUpperCase() + text.slice(1);
            },
            async openToast(msg) {
                const toast = await toastController
                    .create({
                    message: msg,
                    duration: 2000,
                    color: 'danger',
                    cssClass: 'ion-text-center'
                    })
                return toast.present();
            }
        },
        watch: {
            city(){
                this.fetchWeather()
            }
        },
    });
</script>

<style scoped>
.fa-thermometer-half{
    color:lightsalmon;
}
.fa-wind {
    color:lightgrey;
}
.fa-tint{
    color:lightblue;
}
</style>