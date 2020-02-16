<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>
          ZipInfo
        </ion-title>
      </ion-toolbar>
     
    </ion-header>
    <ion-content class="ion-padding">
      <ZipSearch v-on:zip="getZipInfo"/>
      <ZipInfo v-bind:info="info"/>
      <ClearInfo v-bind:info="info" v-on:clear-info="clearInfo" />
    </ion-content>
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
import ZipSearch from '@/components/ZipSearch';
import ZipInfo from '@/components/ZipInfo';
import ClearInfo from '@/components/ClearInfo';

export default {
  name: 'Home',
  components: {
    ZipSearch,
    ZipInfo, 
    ClearInfo
  },
  data() {
    return {
      info: null
    }
  },
  methods: {
    async getZipInfo(zip){
      const response = await fetch(`https://api.zippopotam.us/us/${zip}`);
      if( response.status == 404 ){
        this.showAlert();
      }

      const info = await response.json();
      this.info = info;
    },
     showAlert(){
            return this.$ionic.alertController
            .create({
                header: "Not valid",
                message: "That isn't a valid zip code",
                buttons: ['OK']
            })
            .then(a => a.present())
      },
      clearInfo(){
        this.info = null; 
      }
  }
}
</script>
