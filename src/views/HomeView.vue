<script setup lang="ts">

</script>

<template>
  
        
 
    
        <div class="flex items-center justify-center max-w-screen-3xl w-auto  flex-wrap  mx-auto p-4 bg-transparent  backdrop-blur-[11px] backdrop-saturate-[100%] border border-b-transparent border-t-transparent border-l-transparent border-r-transparent rounded-t-[16px] shadow-[0_8px_32px_0_rgba(0,0,0,0.2)]">
                 
               
            <div class="flex flex-col items-center justify-center w-screen h-screen mx-4 ">
               
                 
    
                    <div class="max-w-screen-xl flex flex-wrap items-center justify-end mx-auto p-4 bg-transparent backdrop-blur-[11px] backdrop-saturate-[100%]  rounded-[16px] shadow-[0_8px_32px_0_rgba(0,0,0,0.2)]">
                      <nav class="bg-transparent w-screen z-20 top-0 start-0 ">
                    <div class="max-w-screen-xl flex flex-wrap items-center justify-end mx-auto p-4 bg-transparent">
                      
                    <div class="items-center justify-between hidden w-full md:flex md:w-auto md:order-1" id="navbar-user">
                        
                      
                      <ul class="font-medium flex flex-col p-4 md:p-0 mt-4 border border-default rounded-base bg-transparent md:flex-row md:space-x-15 rtl:space-x-reverse md:mt-0 md:border-0 md:bg-transparent">
                          <li>
                            <RouterLink to="/" class="block py-2 px-3 text-white bg-brand rounded md:bg-transparent md:text-fg-brand md:p-0" >Home</RouterLink>
                          </li>
                          <li>
                           <RouterLink to="/about" class="block py-2 px-3 text-heading rounded hover:bg-neutral-tertiary md:hover:bg-transparent md:border-0 md:hover:text-fg-brand md:p-0 md:dark:hover:bg-transparent">About</RouterLink>
                          </li>
                          <li>
                            <a href="#" class="block py-2 px-3 text-heading rounded hover:bg-neutral-tertiary md:hover:bg-transparent md:border-0 md:hover:text-fg-brand md:p-0 md:dark:hover:bg-transparent">Services</a>
                          </li>
                          <li>
                            <a href="#" class="block py-2 px-3 text-heading rounded hover:bg-neutral-tertiary md:hover:bg-transparent md:border-0 md:hover:text-fg-brand md:p-0 md:dark:hover:bg-transparent">Pricing</a>
                          </li>
                          <li>
                            <a href="#" class="block py-2 px-3 text-heading rounded hover:bg-neutral-tertiary md:hover:bg-transparent md:border-0 md:hover:text-fg-brand md:p-0 md:dark:hover:bg-transparent">Contact</a>
                          </li>
                        </ul>
                      </div>
                      
                      </div>
                    </nav>
                        <div class="flex flex-row h-150 w-screen ">
                          <section class="flex flex-col h-120 md:h-full  w-xl " >
                              <div class="flex h-full w-full flex-col items-start justify-center gap-4 px-6 text-center font-sans">
                                <h1 class="mb-4 text-7xl font-semibold tracking-tight">
                                  <span class="text-green-400" ref="el"></span>
                                
                                </h1>
                                <h1 class="mb-4 text-5xl font-bold text-blue-400"> Francis</h1>
                                <p class="text-2xl  font-semibold text-white ">I'm a web developer passionate about building modern, responsive, and user-friendly websites with clean code and creative design.</p>
                              </div>
                            </section>
                          <section class="flex flex-col h-150 w-auto content-center md:h-full " >
                              <div class="flex h-full w-full flex-col items-start justify-center gap-8 px-6  text-center font-sans" >
                                  <img src="../assets/avatar2.png" class="">
                               
                              </div>
                            </section>
                            
                        </div>
                        
                    </div>
                 
              </div>
                  
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
    loop: true
  })
})

onBeforeUnmount(() => typed?.destroy())
</script>
