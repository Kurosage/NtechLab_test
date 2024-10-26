

<template>


  <main class="main">
      <p class="main__text_save-process" v-if="saveProcessing">Информация сохраняется</p>
      <my-form :item="item" @save="v => saveHandler(v)" :disabled="saveProcessing"></my-form>
  </main>
</template>
<script setup>
import MyForm from './components/my-form.vue'
import { ref } from 'vue';
const item = ref({"name":"Иван",age:10})
const newItem = ref(null)
const saveProcessing = ref(false)

async function saveHandler(value){
  saveProcessing.value = true
  try{
 
    await new Promise((resolve)=>{setTimeout(resolve,5000)})
  }catch(error){
    console.log( error)
  }finally{
    
    saveProcessing.value = false
  }
  

  
  newItem.value = value
}
</script>

<style scoped>
.main{
  display:flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.main__text_save-process{
  font-size: bold;
  color:red;
 
  
  font-size: 25px;
  margin:  25px;
}
</style>
