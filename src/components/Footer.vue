<template>
  <div id="footer">
    <div id="effect_holder" data-scroll data-scroll-speed="1" data-scroll-direction="horizontal">
      <p id="mouse_over">      
        Merci du passage
      </p>
      <p id="top_text">      
        Merci du passage
      </p>
      <p id="bot_text">      
        Merci du passage
      </p>
    </div>    
    <p id="end" data-scroll data-scroll-speed="-6" data-scroll-direction="horizontal">
      Si tu as apprécié la promenade, viens jeter un œil à mon portefolio !
    </p>
    <a id="portefolio" href="https://wizer21.github.io/" target="_blank" data-scroll data-scroll-speed="3" data-scroll-direction="horizontal">
      <p id="portefolio_text_border">
        Jeter un oeil
      </p>
      <p id="portefolio_text">
        Jeter un oeil
      </p>
    </a>
  </div>
</template>

<script>
export default {
  name: 'Footer',
  mounted(){
    document.getElementById('bot_text').style.setProperty('--float_anim', this.$style["float_anim"])

    let mouse_over = document.getElementById('mouse_over')
    let top_text = document.getElementById('top_text')

    mouse_over.addEventListener('mousemove', event => {
      let rect = mouse_over.getBoundingClientRect()
      let x_converter = rect.width / 100
      let y_converter = rect.height / 100

      top_text.style.clipPath = `circle(5% at ${event.offsetX / x_converter}% ${event.offsetY / y_converter}%`
    })
    
    let portefolio = document.getElementById('portefolio')
    let portefolio_text = document.getElementById('portefolio_text')
    portefolio.addEventListener('mouseenter', () => {
      portefolio_text.style.clipPath = "inset(20% 0 0 0)"
    })    
    portefolio.addEventListener('mouseleave', () => {
      portefolio_text.style.clipPath = "inset(75% 0 0 0)"
    })
  }
}
</script>

<style scoped>
#footer
{
  position: relative;
  width: 100vw;

  background-color: #0f0f0f;

  display: flex;
  align-items: center;
  flex-direction: column;
}
#effect_holder
{
  display: grid;
}
#effect_holder p
{
  grid-column: 1;
  grid-row: 1;

  font-size: 10vw;
}
#mouse_over
{
  color: #1f1f1f;
  cursor: none;
}
#top_text
{
  color: #428a3b;
  clip-path: circle(0% at 0% 0%);
  pointer-events: none;

  transition-timing-function: ease-in-out;
}
#bot_text
{
  color: #428a3b;
  animation: var(--float_anim) 1s infinite ease-in-out alternate;
  pointer-events: none;
}
#end
{
  font-size: 2em;
  margin-right: auto;
  margin-left: 10vw;
}
#portefolio
{
  margin: 2em;
  text-decoration: none;

  display: grid;
}
#portefolio_text_border
{
  color: #1f1f1f;
  font-size: 7vw;
  margin: 0px;

  grid-column: 1;
  grid-row: 1;
}
#portefolio_text
{
  color: #428a3b;
  font-size: 7vw;
  grid-column: 1;
  grid-row: 1;
  margin: 0px;

  transition-duration: 1s;
  clip-path: inset(75% 0 0 0);
}
@media screen and (max-width: 800px) {  
  #adansonii_body
  {
    flex-direction: column;
  }
  #adansonii_stack
  {
    width: 20em;
  }
  #end
  {
    margin-left: 5em;
  }
  #portefolio
  {
    margin-right: 5em;
  }
}
</style>

<style module>
@keyframes float_anim {
  0%{
    clip-path: polygon(3% 68%, 11% 65%, 26% 65%, 36% 73%, 53% 76%, 68% 70%, 78% 68%, 93% 67%, 100% 70%, 100% 100%, 0% 100%, 0 69%);
  }
  100%{
    clip-path: polygon(11% 73%, 22% 77%, 34% 77%, 47% 70%, 58% 65%, 69% 59%, 86% 57%, 100% 60%, 100% 76%, 100% 100%, 0% 100%, 0 62%);
  }
}
</style>