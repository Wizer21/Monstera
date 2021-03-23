<template>
  <div id="variegata">
    <div id="variegata_title_container">
      <h2 id="variegata_title" data-scroll data-scroll-speed="-0.2" data-scroll-direction="horizontal">
        Variegata
      </h2>
      <div id="image_follow">      
        <img :src="require('../assets/images/feuille-duo.png')" alt="monstera" id="floating_image" @load="loaded">
      </div>
      <h2 id="title_copy" data-scroll data-scroll-speed="0.2" data-scroll-direction="horizontal">
        Variegata
      </h2>
    </div>
    <div id="p1" data-scroll data-scroll-speed="-1" data-scroll-direction="vertical">
      <div id="variegata_leaf_container">
        <img :src="require('../assets/images/variegata_leaf.jpg')" alt="monstera variegata" id="variegata_leaf" @load="loaded">
      </div>
      <p data-scroll data-scroll-speed="1" data-scroll-direction="horizontal">
        La Variegata est reconnaissable à ses feuilles panachées.
      </p>
    </div>
    <div id="p2">
      <p data-scroll data-scroll-speed="-2" data-scroll-direction="horizontal">
        Ces taches blanches ne peuvent pas absorber la lumière, il lui faut donc deux fois plus de lumière pour la photosynthèse.     
      </p>
      <div id="scene_container">
        <div id="scene_3d">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import * as THREE from 'three';

export default {
  name: "Variegata",
  methods: {
    loaded(){
      this.$emit('newload')
    }
  },
  mounted(){
    document.getElementById('variegata_leaf_container').style.setProperty('--rotate_loop', this.$style["rotate_loop"])
    document.getElementById('variegata_leaf').style.setProperty('--anti_rotate_loop', this.$style["anti_rotate_loop"])

    // Title hover
    let variegata_title = document.getElementById('variegata_title')
    let image_follow = document.getElementById('image_follow')
    let floating_image = document.getElementById('floating_image')

    variegata_title.addEventListener('mouseenter', () => {
      image_follow.style.opacity = `1`   
      floating_image.style.animation = `${this.$style.flag} 2s infinite alternate ease-in-out`
      floating_image.style.filter = "blur(0px)"
    })    
    variegata_title.addEventListener('mouseleave', () => {
      image_follow.style.opacity = `0`   
      floating_image.style.animation = ""
      floating_image.style.filter = "blur(5px)"
    })
    variegata_title.addEventListener('mousemove', event => {
      let vw = window.innerWidth / 10
      image_follow.style.transform = `translate(${event.offsetX - vw}px, ${event.offsetY - vw}px) rotate(${event.offsetX / 30}deg)`   
    })
    
    // 3D Scene
    const three_scene = document.getElementById('scene_3d')

    let scene = new THREE.Scene()
    
    let light = new THREE.HemisphereLight()
    light.intensity = 1
    scene.add(light)

    const loader = new THREE.TextureLoader();
    const geometry = new THREE.CylinderGeometry( 10, 10, 16, 50 );
    const material = new THREE.MeshBasicMaterial( {transparent: true, map: loader.load(require("../assets/images/variegata.png"))} );
    const cylinder = new THREE.Mesh( geometry, material );
    scene.add( cylinder );

    const camera = new THREE.PerspectiveCamera(
        75,
        1,
        0.1,
        100
    )
    camera.position.set(10, 0, 17)
    camera.rotation.z = 45 * Math.PI / 180
    camera.lookAt(0, 0, 0)

    let renderer = new THREE.WebGLRenderer({ alpha: true , antialias: true })
    renderer.setClearColor( 0x000000, 0 )
    three_scene.appendChild(renderer.domElement)
    
    if( window.innerWidth > 800){
      let vw = window.innerWidth / 3
      renderer.setSize(vw, vw)
    }
    else{      
      let vw = window.innerWidth / 1.6
      renderer.setSize(vw, vw)
    }

    let cylinder_pos = 1
    let cylinder_pos_target = 1
    let rotation = 0

    const animate = function () {
      requestAnimationFrame(animate)
      if (cylinder){
        rotation = (cylinder_pos_target - cylinder_pos) * 0.02
        cylinder_pos += rotation

        cylinder.rotation.y += rotation
      }
      renderer.render(scene, camera)
    }
    animate()

    // Object rotation
    let variegata = document.getElementById('variegata')
    variegata.addEventListener('mousemove', event  => {
      if(cylinder){ 
        let multiplicator = window.innerWidth / 5
        cylinder_pos_target = 2 + event.offsetX / multiplicator
      }

    })
  }
};
</script>

<style scoped>
#variegata {
  width: 100vw;
  background-color: #2f4d2c;

  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
/* HEADER */
#variegata_title_container {
  display: grid;
  margin-top: 2em;
  margin-bottom: 2em;
}
#variegata_title{
  font-size: 15vw;
  z-index: 10;
  margin: 0px;

  grid-row: 1;
  grid-column: 1;

  mix-blend-mode: soft-light;
}
#title_copy
{
  font-size: 15vw;
  z-index: 1;
  margin: 0px;

  grid-row: 1;
  grid-column: 1;
  pointer-events: none;
}
#image_follow {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 5;

  height: 20vw;
  width: 20vw;
  opacity: 0;

  transition: opacity 1000ms, transform 400ms;

  transition-timing-function: ease-out;
}
#floating_image
{
  object-fit: cover;
  height: 100%;
  width: 100%;

  transition-duration: 500ms;
  filter: blur(5px);
}
/* BODY */
/* PART 1 */
#p1
{
  display: flex;
  flex-direction: row;
  pointer-events: none;
}
#variegata_leaf_container
{
  margin: 4vw;
  width: 40em;
  height: 40em;

  clip-path: polygon(61% 7%, 55% 6%, 50% 6%, 43% 7%, 42% 7%, 37% 8%, 31% 10%, 26% 12%, 21% 15%, 17% 18%, 14% 21%, 10% 26%, 7% 32%, 4% 38%, 2% 44%, 1% 49%, 1% 55%, 2% 59%, 3% 66%, 3% 68%, 4% 72%, 6% 76%, 8% 80%, 10% 82%, 13% 85%, 16% 87%, 19% 89%, 23% 92%, 27% 95%, 31% 97%, 33% 98%, 38% 99%, 40% 99%, 44% 99%, 50% 98%, 55% 97%, 59% 96%, 62% 95%, 68% 92%, 73% 89%, 78% 86%, 81% 83%, 85% 78%, 87% 74%, 89% 70%, 92% 65%, 94% 61%, 96% 55%, 97% 49%, 97% 44%, 96% 38%, 95% 33%, 92% 27%, 90% 24%, 87% 20%, 83% 16%, 78% 13%, 71% 10%, 67% 9%);
  animation: var(--rotate_loop) 25s infinite linear;
}
#variegata_leaf
{
  object-fit: contain;
  width: 100%;
  height: 100%;
  animation: var(--anti_rotate_loop) 25s infinite linear;
}
#p1 p {
  margin: 1em;
  font-size: 2em;
  margin-top: 25vh;

  width: 25%;
}
#p2
{
  width: 100vw;
  pointer-events: none;

  display: flex;
  flex-direction: row;
}
#p2 p 
{
  margin-left: 20vw;
  margin-top: 5vw;
  font-size: 2em;
  width: 25%;
}
#scene_3d
{
  pointer-events: none;
  transform: rotate(-25deg) translate(10vw, -10vw);
}
#scene_container
{
  margin: 4em;
}
@media screen and (max-width: 800px) {  
  #p1
  {
    flex-direction: column;
    margin-top: 10vh;
  }  
  #p1 p
  {
    padding: 10%;
    width: 80%;
    margin-top: 0vh;
  }
  #p2
  {  
    flex-direction: column;
  } 
  #p2 p
  {
    padding-top: 10%;
    width: 80%;
  }
  #variegata_leaf_container
  {
    width: 25em;
    height: 25em;
  }
}
</style>

<style module>
@keyframes flag{
  0%{
    transform: skew(0deg, 0deg);
  }
  100%{
    transform: skew(5deg, 0deg); 
  }
}
@keyframes rotate_loop {
  0%{
    transform: rotate(0deg);
  }
  100%{
    transform: rotate(360deg);
  }
}
@keyframes anti_rotate_loop {  
  0%{
    transform: rotate(360deg);
  }
  100%{
    transform: rotate(0deg);
  }
}
</style>