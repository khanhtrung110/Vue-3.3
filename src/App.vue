<script setup lang="ts">
import { ref, watch } from 'vue'
import TheWelcome from './components/TheWelcome.vue'
const number = ref('3123214');
const number2 = ref(0);
const objectProps = ref({
  number: 0
})
// watch(() => number.value,(val) => {
//   console.log(val);

// })
watch(() => objectProps.value.number, (val) => {
  console.log('val--->', val);

}, { deep: true })

const handleChange = (val:string) => {
  console.log(val);
}
watch(()=>number2.value,(val) => {
  console.log('numberApp',val);
  
},{deep:true})
</script>

<template>
  <main>
    <TheWelcome v-model="number" :number2=number2 extraProp='1234'  :objectProps="objectProps"  @change="handleChange"/>
    <button style="padding: 5px; background-color: beige;" @click="number2++">APP CLICK</button>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
