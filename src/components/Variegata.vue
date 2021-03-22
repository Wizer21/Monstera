<template>
  <div id="variegata">
    <div id="variegata_title_container">
      <h2 id="variegata_title" data-scroll data-scroll-speed="-0.2" data-scroll-direction="horizontal">
        Variegata
      </h2>
      <div id="image_follow">      
        <img :src="require('../assets/images/feuille-duo.png')" alt="monstera" id="floating_image">
      </div>
      <h2 id="title_copy" data-scroll data-scroll-speed="0.2" data-scroll-direction="horizontal">
        Variegata
      </h2>
    </div>
    <div id="variegata_container">
      <div id="p1" data-scroll data-scroll-speed="-2" data-scroll-direction="vertical">
        <div id="variegata_leaf_container">
          <img :src="require('../assets/images/variegata_leaf.png')" alt="monstera variegata" id="variegata_leaf">
        </div>
        <p data-scroll data-scroll-speed="1" data-scroll-direction="horizontal">
          La Variegata est reconnaissable à ses feuilles panachées.
        </p>
      </div>
      <div id="p2">
        <p data-scroll data-scroll-speed="-2" data-scroll-direction="horizontal">
          Ces tâches blanches ne peuvent pas absorber la lumière, il lui faut donc deux fois plus de lumière pour la photosynthèse.     
        </p>
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
  mounted(){
    document.getElementById('variegata_leaf').style.setProperty('--circle_float', this.$style["circle_float"])

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
    const geometry = new THREE.CylinderGeometry( 10, 10, 10, 50 );
    const material = new THREE.MeshBasicMaterial( {transparent: true, map: loader.load(require("../assets/images/multiples_variegata.png"))} );
    const cylinder = new THREE.Mesh( geometry, material );
    scene.add( cylinder );

    const camera = new THREE.PerspectiveCamera(
        75,
        window.innerWidth / window.innerHeight,
        0.1,
        100
    )
    camera.position.set(10, 0, 15)
    camera.rotation.z = 45 * Math.PI / 180
    camera.lookAt(0, 0, 0)

    let renderer = new THREE.WebGLRenderer({ alpha: true , antialias: true })
    renderer.setClearColor( 0x000000, 0 )
    three_scene.appendChild(renderer.domElement)
    
    let vw = window.innerWidth / 3
    renderer.setSize(vw, vw)

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
  margin: 8vw;
  width: 35vw;
  height: 35vw;
}
#variegata_leaf
{
  object-fit: contain;
  width: 100%;
  height: 100%;
  animation: var(--circle_float) 5s infinite ease-in-out alternate;
}
#p1 p {
  margin: 2vw;
  margin-top: 15vw;
  font-size: 3em;

  width: 15vw;
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
  font-size: 3em;
  width: 25vw;
}
#scene_3d
{
  pointer-events: none;
  transform: rotate(-25deg) translate(10vw, -10vw);
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
@keyframes circle_float {
  0%{
    clip-path: polygon(4% 50%, 4% 46%, 5% 41%, 7% 37%, 9% 33%, 11% 29%, 13% 26%, 16% 23%, 20% 19%, 24% 17%, 25% 17%, 30% 16%, 32% 14%, 37% 12%, 39% 11%, 45% 9%, 49% 9%, 52% 8%, 56% 9%, 60% 10%, 65% 10%, 70% 11%, 73% 12%, 77% 13%, 81% 13%, 84% 15%, 87% 18%, 89% 20%, 91% 22%, 92% 25%, 94% 28%, 94% 31%, 94% 34%, 95% 37%, 95% 40%, 95% 42%, 95% 44%, 94% 46%, 94% 49%, 94% 53%, 94% 57%, 94% 61%, 94% 65%, 92% 70%, 90% 73%, 88% 77%, 86% 80%, 84% 83%, 81% 86%, 78% 90%, 75% 92%, 71% 94%, 68% 97%, 64% 97%, 62% 98%, 60% 98%, 57% 99%, 55% 98%, 52% 98%, 48% 98%, 44% 97%, 41% 97%, 38% 97%, 35% 96%, 31% 96%, 28% 95%, 24% 94%, 20% 93%, 17% 92%, 12% 89%, 10% 87%, 8% 84%, 6% 82%, 5% 79%, 4% 76%, 3% 73%, 3% 71%, 3% 66%, 3% 63%, 4% 60%, 4% 56%, 4% 54%);
  }
  100%{
    clip-path: polygon(7% 50%, 6% 45%, 7% 40%, 9% 37%, 10% 33%, 11% 29%, 12% 24%, 15% 17%, 19% 14%, 23% 11%, 27% 8%, 31% 6%, 35% 5%, 39% 6%, 43% 7%, 47% 8%, 49% 7%, 52% 7%, 56% 6%, 59% 7%, 63% 8%, 68% 8%, 73% 9%, 78% 10%, 81% 12%, 84% 13%, 87% 16%, 88% 18%, 90% 21%, 92% 25%, 93% 28%, 93% 32%, 93% 35%, 94% 38%, 94% 42%, 94% 45%, 91% 49%, 90% 53%, 90% 56%, 90% 59%, 90% 63%, 90% 66%, 91% 69%, 89% 72%, 88% 75%, 86% 78%, 85% 82%, 83% 85%, 81% 88%, 79% 91%, 75% 94%, 71% 95%, 68% 97%, 64% 97%, 62% 98%, 60% 98%, 57% 99%, 55% 98%, 52% 98%, 48% 98%, 44% 97%, 42% 96%, 39% 95%, 37% 95%, 32% 94%, 29% 93%, 24% 93%, 20% 92%, 17% 89%, 14% 87%, 11% 85%, 10% 83%, 8% 82%, 5% 79%, 4% 76%, 3% 73%, 3% 71%, 3% 66%, 3% 63%, 4% 60%, 5% 57%, 5% 54%);
  }
}
</style>