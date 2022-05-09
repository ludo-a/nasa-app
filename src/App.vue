<template>
  <div id="headtitle">
    <figure>
        <img id="logonasa" :src="logourl"  />   
    </figure>
    <h1>APOD</h1>
    <div id="headtitlevue">
      <h4>CREATED WITH</h4>
      <figure id="logovuebox">
        <img id="logovue" :src="logovue"  />   
      </figure>
    </div>
  </div> 
  <div>
    <a id="haut"></a>
    <h1 id="titleApp">Astronomy Picture Of the Day</h1>
  </div>

  <Modal v-show="open" @close-modal="open = false">
        <template #title>Made with Vue.js V3.0</template>
        <template #default>
            Upgrade to Vue 3.0 at <a target="_blank" href="https://www.training-dev.fr/Cours/Les-bases-de-Vue.JS-3" >training-dev.fr</a>
        </template>
  </Modal>
  <Slider :slides="photos">
    <template v-slot:default="slotProps">
      <Photo class="photoCss"
        :key="slotProps.slide.key" 
        :url="slotProps.slide.url" 
        :title="slotProps.slide.title"
        :explanation="slotProps.slide.explanation"
        :media_type="slotProps.slide.media_type"
        :copyright="slotProps.slide.copyright"
        :date="new Date(slotProps.slide.date)"
      ></Photo>
    </template>
  </Slider>
  <button @click="open = !open" class="buttonSlider"><i class="fa-solid fa-question fa-2xl"></i></button>
</template>

<script>
import Photo from './components/Photo.vue'
import Slider from './components/Slider.vue'
import logourl from './assets/nasalogo.png'
import logovue from './assets/logo.png'
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    Photo, Slider, Modal
  },
  data() {
    return {
      photos: [],
      open:false,
      logourl: logourl,
      logovue: logovue
    }
  },
  created() {
    let dateactuel = new Date();
    let moisactuel = dateactuel.getMonth()+1;
    let jouractuel = dateactuel.getDate();
    
//date actuel
    if(moisactuel < 10)
    {
      moisactuel = "0"+ moisactuel;
    }

    if(jouractuel < 10)
    {
      jouractuel = "0"+ jouractuel;
    }

//calcul du mois et jour pour la date de départ de la requete API (-4 jours) 
  
  let jourdepart = jouractuel-4;
  let moisdepart = moisactuel;
  if((jourdepart <= 1 || jourdepart == 2) && (moisdepart != 1))
  {
      jourdepart = 30;
      moisdepart -=1;
      moisdepart = "0"+ moisdepart;
  }

  if((jouractuel <= 1 || jouractuel == 2) && (moisdepart == 1))
  {
      jourdepart = 30;
      moisdepart = 12;
  }

  if((jouractuel <= 1 || jouractuel == 2) && (moisdepart == 2))
  {
      jourdepart = 24;
      moisdepart = "01";
  }
  
    let startdate = dateactuel.getFullYear()+"-"+moisdepart+"-"+jourdepart;
    let dateactuelfinal = dateactuel.getFullYear()+"-"+moisactuel+"-"+jouractuel;
    
    const API_URL = `https://api.nasa.gov/planetary/apod?start_date=${startdate}&end_date=${dateactuelfinal}&api_key=Hy9WuTGrIlb6rBISBGQ1GAjNkujmdxd3JCdznmMC`

    fetch(API_URL)
    .then(result => result.json())
    .then(result => {
      this.photos = result;
    })
  },
}
</script>

<style>

@font-face {
 font-family: "nasalization";
 src: url("./assets/nasalization-rg.otf") format("opentype");
}

body{
  background-color: #2c3e5081;
}

html {
  scroll-behavior: smooth;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#logonasa {
  width:260px;
  max-width: 100%;
}

#headtitle{
  display:flex;
  justify-content: center;
  align-items: center;
  border: 8px solid #265ebe;
  border-radius: 20px;
  box-shadow: 6px 10px 5px #fc3e217d;
  margin-bottom:50px;
  background-color: rgba(220, 216, 216, 0.796);
}

h1{
  font-family: "nasalization";
  font-size: 100px;
}

h4{
  font-family: "nasalization";
  margin-bottom:0px;
  margin-top:0px;
  font-size:24px;
}

#titleApp{
  font-family: "nasalization";
  font-size: 40px;
}

#logovuebox{
  margin-top:0px;
  margin-bottom:0px;
}

#logovue{
  max-width: 100%;
}

.photoCss{
  border: 3px solid #fc3e2134;
  background-color: rgba(220, 216, 216, 0.796);
  border-radius: 20px;
  padding: 30px 30px 15px 30px;
  margin-bottom: 30px;
  }

@media screen and (max-width: 800px) {
h1{
    font-size: 60px;
  }

h4{
  font-size: 18px;
  }

#ytplayer{
  width:300px;
  height: 150px;
  }
}

@media screen and (max-width: 600px) {
  #headtitlevue{
    display:none;
  }
  h1{
    margin-right:30px;
  }
}

@media screen and (max-width: 450px) {
  h1,#ytplayer{
    display:none;
  }
}
</style>
