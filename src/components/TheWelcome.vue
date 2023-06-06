<script setup lang="ts" generic="T">
import { watchEffect,watch, toRef,ref, toValue } from 'vue';
export interface IProp<A> {
  modelValue: string;
  number2: A;
  objectProps: Object
}
// Imported and Complex Types Support in Macros
const { number2 } = defineProps<IProp<T> & { extraProp?: T }>();

defineSlots<{
  default?: (props: { msg: string })=> string
}>()
//defineModel
// const number2 = defineModel<number>('number2');
 const modelValue = defineModel();
 //Reactive Props Destructure
 watchEffect(() => {
  console.log('number2',number2);
 })
//  defineEmits
const emit = defineEmits<{
  change: [id: number] // named tuple syntax
  update: [value: string]
}>()

//toRef
// creates a readonly ref that calls the getter on .value access
const testToRef = toRef(() => number2);
const testRef = ref(1);
const testExisting = toRef(() => testRef)
const testToValue = toValue(testRef) ;
console.log('testToValue',testToValue);

watch(()=>testRef,(val) => {
  console.log('testRef',val);
  
},{deep:true})
watch(()=> testToValue,(val)=>{
  console.log('TOVALUE',val);
  
},{deep:true})

</script>

<template>
  <div>
    <h1>TITLE123</h1>
    <button @click="number2++" style="padding: 5px; background-color: aquamarine;">CLICK</button>
    <slot></slot>
  </div>
</template>
