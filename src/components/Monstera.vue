<template>
  <div id="monstera">
    <div id="header">
      <h1 id="main_title">
        Monstera Deliciosa
      </h1>
      <div id="leaf_container">
        <img :src="require('../assets/images/leaf.png')" alt="Monstera leaf" id="main_leaf">
      </div>
    </div>
    <div id="body">
      <div id="leaf_presentation">
        <img :src="require('../assets/images/multiple_leaf.jpg')" alt="Monstera" id="multiple_leaf">
      </div>
      <div id="side">
        <p>
          Monstera deliciosa est une plante originaire des forêts tropicales. Populaire pour ses feuilles gigantesques.
        </p>
        <div id="leaf_name">
          <img :src="require('../assets/images/huge_leaf.jpg')" alt="Monstera" id="huge_leaf">
          <div id="hide_text_container">
            <p id="hide_text">
              Elle tient son nom de la contration de «monstrueux» et «délicieux» due à sa taille pouvant atteindre les 9 mètres.
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Monstera',
  mounted(){

    // Header animation
    let header = document.getElementById('header')
    let leaf_container = document.getElementById('leaf_container')
    let main_leaf = document.getElementById('main_leaf')
    let main_title = document.getElementById('main_title')
    let hide_text = document.getElementById('hide_text')

    header.addEventListener('mousemove', event => {
      let posX = (event.offsetX - (window.innerWidth / 2)) / 3 
      leaf_container.style.transform = `translateX(${posX}px)`
      main_title.style.transform = `translateX(${-posX}px)`

      let posY = (event.offsetY - (window.innerHeight / 2)) / 40 
      main_leaf.style.transform = `rotate(${25 + posY}deg)`

    })

    // Hidden text
    let leaf_name = document.getElementById('leaf_name')
    let hide_text_container = document.getElementById('hide_text_container')

    leaf_name.addEventListener('mouseenter', () => {
      hide_text_container.style.height = "12vw"
      hide_text_container.style.width = "12vw"
      hide_text_container.style.margin = "0vw"
    })
    leaf_name.addEventListener('mouseleave', () => {
      hide_text_container.style.height = "0vw"
      hide_text_container.style.width = "0vw"
      hide_text_container.style.margin = "6vw"
    })
    leaf_name.addEventListener('mousemove', event=> {
      let vw = window.innerWidth / 100
      let x = event.offsetX - (vw * 6)
      let y = event.offsetY - (vw * 6)
      hide_text_container.style.transform = `translate(${x}px, ${y}px)`
      hide_text.style.transform = `translate(${-x}px, ${-y}px)`
    })
  }
}
</script>

<style scoped>
#monstera
{
  width: 100vw;
  background-color: #262626;

  display: flex;
  flex-direction: column;
}
/* HEADER */
#header
{
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
#main_title
{
  position: absolute;
  font-size: 3vw;
  pointer-events: none;

  transition-timing-function: ease-out;
  transition-duration: 1000ms;
}
#leaf_container
{
  position: absolute;
  height: 40vw;
  width: 40vw;
  pointer-events: none;

  transition-timing-function: ease-out;
  transition-duration: 1000ms;
}
#main_leaf
{
  object-fit: contain;
  height: 100%;
  width: 100%;
  transform: rotate(25deg);
  pointer-events: none;

  transition-timing-function: ease-out;
  transition-duration: 500ms;
}
/* BODY */
#body
{
  width: 100vw;
  display: flex;
  align-items: flex-start;
}
#side
{
  margin-top: 20vw;
  width: 20vw;
}
#side p 
{  
  font-size: 2vw;
}
#leaf_presentation
{
  margin: 10vw;
  width: 35vw;
}
#multiple_leaf
{  
  object-fit: contain;
  height: 100%;
  width: 100%;
  pointer-events: none;
}
#leaf_name
{
  margin-top: 5vw;
  margin-bottom: 5vw;
  width: 25vw;  

  display: flex;
}
#huge_leaf
{
  object-fit: contain;
  height: 100%;
  width: 100%;
  pointer-events: none;
}
#hide_text_container
{
  position: absolute;
  height: 0vw;
  width: 0vw;
  background-color: rgb(26, 26, 26, 0.8);
  border-radius: 50%;  
  overflow: hidden;
  pointer-events: none;

  transition: height 400ms, width 400ms, margin 400ms;

}
#hide_text
{
  position: static;
  margin: 3vw;
  width: 19vw;
  pointer-events: none;
}
</style>
