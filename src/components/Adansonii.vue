<template>
  <div>
    <div id="adansonii_header">
    </div>
    <div id="adansonii_body">
      <div>
        <img :src="require('../assets/images/adansonii.jpg')" alt="Monstera leaf" id="main_leaf">
      </div>
      <p>
        Adansonii est elle réputé pour ses petites feuilles perforées et pour sa capacité à grimper partout     
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Adansonii',
  methods: {
    deployTitle(){
      let letters = document.getElementsByClassName('adansonii_letter')

      for (let l of letters){
        l.style.opacity = 1
      }
    }
  },
  mounted(){
    let adansonii_header = document.getElementById('adansonii_header')
    let elem
    let div
    let word = "Adansonii"
    let speedList = [1, -3, 2, -1, 3, 2, 1, 3, -2]

    for (let i = 0; i < word.length ; i++){
      elem = document.createElement('h2')
      elem.textContent = word[i]
      elem.className = "adansonii_letter"

      div = document.createElement('div')
      div.dataset.scroll = ""
      div.dataset.scrollSpeed = speedList[i]
      div.appendChild(elem)

      adansonii_header.appendChild(div)
    }
  }
}
</script>

<style scoped>
#adansonii
{
  width: 100vw;
  background-color: #1c1c1c;

  display: flex;
  flex-direction: column;
}
/* Header */
#adansonii_header
{
  display: flex;
  justify-content: center;
  align-items: center;

  width: 100vw;
}
/* Body */
#adansonii_body
{
  width: 100vw;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
#adansonii_body img
{
  margin: 5vw;  
}
#adansonii_body p
{
  margin: 5vw;
  width: 20vw;
  font-size: 2vw;
}
</style>

<style>
.adansonii_letter
{
  margin: 0px;
  font-size: 12vw;

  transition: opacity 500ms, transform 1000ms;
  opacity: 0;

}
.adansonii_letter:hover
{
  transition-duration: 200ms;
  transform: translateY(-2vh);
}
</style>