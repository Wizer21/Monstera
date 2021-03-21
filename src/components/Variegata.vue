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
          <img :src="require('../assets/images/variegata_leaf.png')" alt="monstera variegata">
        </div>
        <p data-scroll data-scroll-speed="1" data-scroll-direction="horizontal">
          La Variegata est reconnaissable à ses feuilles panachées.
        </p>
      </div>
      <div id="p2">
        <p data-scroll data-scroll-speed="-2" data-scroll-direction="horizontal">
          Ces tâches blanches ne peuvent pas absorber la lumière, il lui faut donc deux fois plus de lumière pour la photosynthèse      
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
    // Title hover
    let variegata_title = document.getElementById('variegata_title')
    let image_follow = document.getElementById('image_follow')
    let floating_image = document.getElementById('floating_image')

    variegata_title.addEventListener('mouseenter', () => {
      image_follow.style.opacity = `1`   
      floating_image.style.animation = `${this.$style.flag} 2s infinite alternate ease-in-out`
    })    
    variegata_title.addEventListener('mouseleave', () => {
      image_follow.style.opacity = `0`   
      floating_image.style.animation = ""
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

  transition: opacity 1000ms;
}
#image_follow img
{
  object-fit: cover;
  height: 100%;
  width: 100%;
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
}
#variegata_leaf_container img
{
  object-fit: contain;
  width: 100%;
  height: 100%;
}
#p1 p {
  margin: 2vw;
  margin-top: 15vw;
  font-size: 2vw;

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
  font-size: 2vw;
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
</style>