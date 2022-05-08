<template >
  <Renderer ref="rendererC" antialias resize="window">
    <Camera :position="{ x: xPos, y: 2, z:zPos+10}" />
    <div class="score absolute text-gray-800 text-7xl font-semibold" style="left:50%; transform:translate(-50%,-50%); top:10%;">{{Math.round(counter)}}</div>
    <Scene background="#fff">
       <PointLight :position="{x:0 , y:10 , z:10 }" :intensity="1000" :cast-shadow="true"></PointLight>
      <AmbientLight :position="{ y: -50, z: -50 }" :intensity="0.6" /> 
      <Box :width="10" :depth="1000" :height="0.1">
              <BasicMaterial color="#f7f7f7" />
      </Box>
      <Box :position="{ x: xPos, y: yPos, z: zPos }" ref="Player" style="transition:0.6s ease;">
        <BasicMaterial color="#f53643" />
      </Box>
    </Scene>
  </Renderer>
</template>

<script setup>
//imports
import { ref, onMounted , h } from 'vue'
import { Box, Camera, LambertMaterial , AmbientLight, BasicMaterial , EffectComposer, RenderPass, UnrealBloomPass, FilmPass, HalftonePass, GltfModel, PointLight, Renderer, Scene } from 'troisjs'
import {Clock} from 'three'

//declarations
const rendererC = ref()
let xPos = ref(0)
let yPos = ref(0.5)
let zPos = ref(0)
let clock = new Clock()
let counter = ref(0)


//movement-specific
let delta = ref(0)
let speed = ref(10)
let Player = ref(null)



//logic
document.addEventListener('keydown', key => {
  console.log(key.code)
  if (key.key == "ArrowLeft") {
    xPos.value -= speed.value*delta.value
  }
  if (key.key == "ArrowRight") {
    xPos.value += speed.value*delta.value
  }
})
//mounted
onMounted(() => {
  const renderer = rendererC.value
  renderer.onBeforeRender(() => {
    delta.value = clock.getDelta()
    counter.value += 0.1
   zPos.value -= 0.4
  })
});
</script>

<style>
body {
  margin: 0;
}

canvas {
  height:98vh;
  width:98vw;
  position:absolute;
  top:50%;
  left:50%;
  transform:translate(-50% , -50%);
}
</style>