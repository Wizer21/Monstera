<template>
  <div>
    <div id="adansonii_header">
    </div>
    <div id="adansonii_body">
      <div id="adansonii_stack">
        <img :src="require('../assets/images/adansonii.jpg')" alt="adansonii" id="adansonii_stack_img">
      </div>
      <p id="adansonii_text">
        Adansonii est elle réputée pour ses petites feuilles perforées et pour sa capacité à grimper partout     
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
    // Animated letters
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
  
    // Animated Body
    let adansonii_stack = document.getElementById('adansonii_stack')
    let adansonii = document.getElementById('adansonii')
    let adansonii_text = document.getElementById('adansonii_text')
    let isHold = false

    let last_x = 0
    let last_y = 0
    let pos_x = 0
    let pos_y = 0
    
    adansonii_stack.addEventListener('mouseenter', event => {
      isHold = true
      last_x = event.offsetX
      last_y = event.offsetY
      pos_x = 0
      pos_y = 0
    }) 
    adansonii_stack.addEventListener('mouseleave', () => {
      isHold = false
      adansonii_stack.style.transform = "translate(0px, 0px)"
      adansonii_text.style.transform = "translate(0px, 0px)"
      adansonii_stack.style.clipPath = "circle(100% at 50% 50%)"
    }) 

    adansonii.addEventListener('mousemove', event => {
      if (isHold){
        pos_x += event.offsetX - last_x
        pos_y += event.offsetY - last_y

        let size = 100
        if(pos_x < 0){
          size += pos_x / 4
        }
        else{
          size -= pos_x / 4
        }
        if(pos_y < 0){
          size += pos_y / 4
        }
        else{
          size -= pos_y / 4
        }

        adansonii_stack.style.transform = `translate(${pos_x}px, ${pos_y}px)`
        adansonii_text.style.transform = `translate(${-pos_x}px, ${-pos_y}px)`
        adansonii_stack.style.clipPath = `circle(${size}% at 50% 50%)`

        last_x = event.offsetX
        last_y = event.offsetY
      }
    })
  }
}
</script>

<style scoped>
#adansonii
{
  width: 100vw;
  min-height: 100vh;
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

  width: 100%;
  margin-top: 3em;
  margin-bottom: 2em;
}
/* Body */
#adansonii_body
{
  width: 100vw;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin-top: 5em;
  margin-bottom: 5em;
}
#adansonii_stack
{
  position: relative;
  width: 16em;

  transition-duration: 1000ms;
  transition-timing-function: ease-out;
}
#adansonii_text
{
  position: relative;
  transition-duration: 2000ms;
  transition-timing-function: ease-out;
  pointer-events: none;

  margin: 2em;
  width: 10em;
  font-size: 2em;
}
#adansonii_stack_img
{
  object-fit: contain;
  width: 100%;
  height: 100%;
  
  margin: 0px;
  cursor: pointer;

  /* Prevent user pick */
  user-drag: none; 
  user-select: none;
  -moz-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;
  -ms-user-select: none;

  pointer-events: none;
}
@media screen and (max-width: 800px) {  
  #adansonii_body
  {
    flex-direction: column;
  }
}
</style>

<style>
.adansonii_letter
{
  margin: 0px;
  font-size: 12vw;

  transition: opacity 1000ms, transform 1000ms;
  opacity: 0;
}
.adansonii_letter:hover
{
  transition-duration: 200ms;
  transform: translateY(-2vh);
}
</style>