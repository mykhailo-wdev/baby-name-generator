<template>
    <div class="card">
        <h4>{{ name }}</h4>
        <p @click="removeName">x</p>
    </div>
</template>

<script setup lang="ts">
interface NameProps {
  name: string,
  idx: number
}
const props = defineProps<NameProps>()


const emit = defineEmits(['remove'])

const removeName = () => {
  emit('remove', props.idx)
}
</script>

<style>
.card {
  background-color: rgb(27, 60 , 138);
  width: 28%;
  color: rgb(255, 255, 255);
  border-radius: 0.3rem;
  padding: 0.3rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
  position: relative;
}

.card p {
  position: absolute;
  top: -20%;
  left: 92.5%;
  cursor: pointer;
  color: rgba(255, 255, 255, 0.178);
}
</style>