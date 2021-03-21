<template>
  <div id="adansonii">
    <div id="adansonii_header">
    </div>
    <p>
      La monstera adansonii est réputé pour ses petites feuilles perforées et pour sa capacité à grimper partout     
    </p>
    <div>
      <img :src="require('../assets/images/adansonii.jpg')" alt="Monstera leaf" id="main_leaf">
    </div>
  </div>
</template>

<script>
export default {
  name: 'Adansonii',
  mounted(){
    let adansonii_header = document.getElementById('adansonii_header')
    let elem
    
    for (let letter of "Adansonii"){
      elem = document.createElement('h2')
      elem.textContent = letter
      elem.className = "adansonii_letter"

      adansonii_header.appendChild(elem)
    }

  }
}
</script>

<style scoped>
#adansonii
{
  width: 100vw;
  background-color: #262626;

  display: flex;
  flex-direction: column;
}
#adansonii_header
{
  display: flex;
  justify-content: center;
  align-items: center;

  width: 100vw;
}
</style>

<style>
.adansonii_letter
{
  margin: 0px;
  font-size: 12vw;
  transition-duration: 1000ms;
}
.adansonii_letter:hover
{
  transition-duration: 100ms;
  transform: translateY(-2vh);
}
</style>