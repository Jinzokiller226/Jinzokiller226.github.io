<script setup lang="ts">

</script>

<template>

       
                 <!-- Main Contained Wrapper: Centered on screen, fixed layout boundary, prevents any content spilling out -->
<div class="relative w-full max-w-7xl mx-auto h-[600px] max-h-screen overflow-hidden flex items-center justify-center bg-transparent px-6">
  
  <!-- Side-by-Side Flex Layout Container -->
  <section class="flex flex-col md:flex-row items-center justify-between w-full h-full py-8 gap-8 md:gap-12">
    
    <!-- Left Side: Text Column -->
    <div class="flex flex-col items-start justify-center flex-1 text-left font-sans gap-3 h-full">
      <!-- Typing/Intro Heading -->
     
                               <h1 class="mb-4 text-7xl font-semibold tracking-tight">
                                  <span class="text-green-400" ref="el"></span>
                                
                                </h1>
                                
                                
    
      <!-- Name Display -->
      <h2 class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-bold text-[#3B82F6] mb-1">
        Francis Agustin
      </h2>
      <!-- Description Paragraph -->
      <p class="text-base sm:text-lg md:text-xl text-gray-200 max-w-md leading-relaxed overflow-hidden text-ellipsis">
        I'm a web developer passionate about building modern, responsive, and user-friendly websites with clean code and creative design.
      </p>
      <div class="flex flex-row w-auto gap-8">
      <a href="https://www.linkedin.com/in/francis-agustin-venas-b32a00120/" target="_blank" rel="noopener noreferrer" class="text-white bg-transparent box-border border border-transparent hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 shadow-xs font-medium leading-5 rounded-lg text-sm px-4 py-2.5 focus:outline-none">
                                      <svg class="w-6 h-6 text-gray-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" viewBox="0 0 24 24">
        <path fill-rule="evenodd" d="M12.51 8.796v1.697a3.738 3.738 0 0 1 3.288-1.684c3.455 0 4.202 2.16 4.202 4.97V19.5h-3.2v-5.072c0-1.21-.244-2.766-2.128-2.766-1.827 0-2.139 1.317-2.139 2.676V19.5h-3.19V8.796h3.168ZM7.2 6.106a1.61 1.61 0 0 1-.988 1.483 1.595 1.595 0 0 1-1.743-.348A1.607 1.607 0 0 1 5.6 4.5a1.601 1.601 0 0 1 1.6 1.606Z" clip-rule="evenodd"/>
        <path d="M7.2 8.809H4V19.5h3.2V8.809Z"/>
      </svg>
          </a>
          <a href="https://github.com/jinzokiller226" target="_blank" rel="noopener noreferrer"  class="text-white bg-transparent box-border border border-transparent hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 shadow-xs font-medium leading-5 rounded-lg text-sm px-4 py-2.5 focus:outline-none">
              <svg class="w-6 h-6 text-gray-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" viewBox="0 0 24 24">
              <path fill-rule="evenodd" d="M12.006 2a9.847 9.847 0 0 0-6.484 2.44 10.32 10.32 0 0 0-3.393 6.17 10.48 10.48 0 0 0 1.317 6.955 10.045 10.045 0 0 0 5.4 4.418c.504.095.683-.223.683-.494 0-.245-.01-1.052-.014-1.908-2.78.62-3.366-1.21-3.366-1.21a2.711 2.711 0 0 0-1.11-1.5c-.907-.637.07-.621.07-.621.317.044.62.163.885.346.266.183.487.426.647.71.135.253.318.476.538.655a2.079 2.079 0 0 0 2.37.196c.045-.52.27-1.006.635-1.37-2.219-.259-4.554-1.138-4.554-5.07a4.022 4.022 0 0 1 1.031-2.75 3.77 3.77 0 0 1 .096-2.713s.839-.275 2.749 1.05a9.26 9.26 0 0 1 5.004 0c1.906-1.325 2.74-1.05 2.74-1.05.37.858.406 1.828.101 2.713a4.017 4.017 0 0 1 1.029 2.75c0 3.939-2.339 4.805-4.564 5.058a2.471 2.471 0 0 1 .679 1.897c0 1.372-.012 2.477-.012 2.814 0 .272.18.592.687.492a10.05 10.05 0 0 0 5.388-4.421 10.473 10.473 0 0 0 1.313-6.948 10.32 10.32 0 0 0-3.39-6.165A9.847 9.847 0 0 0 12.007 2Z" clip-rule="evenodd"/>
            </svg>

          </a>
      </div>
                                

                                  
      

    </div>

    <!-- Right Side: Avatar Image Column -->
    <div class="flex items-center justify-center flex-1 w-full h-full max-h-[45%] md:max-h-full overflow-hidden">
      <img 
        src="../assets/avatar2.png" 
        alt="Francis Avatar" 
        class="w-full h-full object-contain max-h-[250px] sm:max-h-[300px] md:max-h-[500px]"
      />
    </div>

  </section>
</div>
                   
    
   

 
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import Typed from 'typed.js'

const el = ref(null)
let typed

onMounted(() => {
  typed = new Typed(el.value, {
    strings: ["Welcome","Hi!, I'm " ],
    typeSpeed: 50,
    backSpeed: 30,
    loop: false
  })
})

onBeforeUnmount(() => typed?.destroy())
</script>
