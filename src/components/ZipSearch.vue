<template>
  <ion-grid>
      <form @submit="submitForm">
          <ion-col>
              <ion-item>
                  <ion-label>
                      Zip code
                  </ion-label>
                  <ion-input name="zip" :value="zip" @input="zip = $event.target.value">

                  </ion-input>
              </ion-item>
              
          </ion-col>
          <ion-col>
             <ion-button type="submit" color="primary" expand="block" placeholder="Enter US zipcode">
                 Find
             </ion-button>
          </ion-col>
      </form>
  </ion-grid>
</template>

<script>
export default {
    name: "ZipSearch",
    data(){
        return {
            zip: ""
        };
    },
    methods: {
        submitForm(e){
            e.preventDefault();

            const isValidZip = /(^\d{5}$)/.test(this.zip);

            if( ! isValidZip ){
                this.showAlert();
                this.zip="";
            } else {
                this.$emit('zip', this.zip);
                this.zip="";
            }
            
        }, 
        showAlert(){
            return this.$ionic.alertController
            .create({
                header: "Enter zip code",
                message: "Please enter a valid zip code",
                buttons: ['OK']
            })
            .then(a => a.present())
        }
    }
}
</script>
