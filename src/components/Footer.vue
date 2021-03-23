<template>
  <div id="footer">
    <div id="effect_holder">
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
  justify-content: center;
  align-items: center;
  flex-direction: column;

  padding: 5vh;
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
  -webkit-text-stroke: 1px #2f4d2c;
  color: transparent;
  cursor: none;
}
#top_text
{
  -webkit-text-stroke: 1px #2f4d2c;
  color: #2f4d2c;
  clip-path: circle(0% at 0% 0%);
  pointer-events: none;

  transition-timing-function: ease-in-out;
}
#bot_text
{
  -webkit-text-stroke: 1px #2f4d2c;
  color: #2f4d2c;
  animation: var(--float_anim) 1s infinite ease-in-out alternate;
  pointer-events: none;
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