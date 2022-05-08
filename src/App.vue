<template>
<Game v-if="!showMenu"/>
<div v-if="showMenu" ref="menu" class="absolute h-full w-full flex flex-col items-center justify-center glass" style="transition:0.6s ease; z-index:1;">
<p class="text-7xl text-center border-b-8 w-80 border-b-[#f53643] font-bold text-gray-800">Box Run</p>
<div class="buttons mt-40 flex flex-col items-center">
<a class="button" @click="play()">PLAY</a><br>
<a class="button" @click="navigate()">VIEW REPOSITORY</a>

</div>
</div>

</template>

<script setup>
import Game from './Game/Game.vue'
import {ref} from 'vue'

const showMenu = ref(true);
const menu = ref(null)

function play(){
  showMenu.value = false
}

function navigate(){
  document.location.href = "https://github.com/vampire-js"
}
</script>


<style>
.button{
padding:10px 20px;
font-weight:500;
border:0.5mm solid #171717;
color:#171717;
transition:0.3s ease;
cursor:pointer;
width:300px;
text-align:center;
}
.button:hover{
    background:rgba(19, 19, 19, 0.06);
}
.glass{
    background: rgba( 255, 255, 255, 0.25 );
box-shadow: 0 8px 32px 0 rgba( 31, 38, 135, 0.37 );
backdrop-filter: blur( 10px );
-webkit-backdrop-filter: blur( 4px );
border-radius: 10px;
border: 1px solid rgba( 255, 255, 255, 0.18 );
}
</style>

