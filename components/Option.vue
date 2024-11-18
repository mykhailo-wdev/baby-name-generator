<template>
    <div class="option-container">
        <h4>{{ option.title }}</h4>
        <div class="option-buttons">
          <button 
            v-for="(value, idx) in option.buttons" :key="`${value}-${idx}`"
            class="option" 
            :class="computeButtonsClasses(value, idx)"
            @click="options[option.category] = value"
            >
            {{ value }}</button>
        </div>
    </div>
</template>

<script setup lang="ts">
import { Gender, Popularity, Length } from '~/data';
  interface OptionProps {
      option: {
          title: string;
          category: keyof OptionProps['options']; // Посилання на ключі
          buttons: Gender[] | Popularity[] | Length[];
      };
      options: {
          gender: Gender;
          popularity: Popularity;
          length: Length;
      };
  }


    const props = defineProps<OptionProps>();

    const computeButtonsClasses = (value: Gender | Popularity | Length, idx: number): string => {
    const classNames: string[] = [];
    if (props.options[props.option.category] === value) {
        classNames.push('option-active');
    }
    if (idx === 0) classNames.push('option-left');
    if (idx === props.option.buttons.length - 1) classNames.push('option-right');
    return classNames.join(' ');
};

    
</script>

<style>
.option-container {
  margin-bottom: 2rem;
}

.option {
  background-color: rgb(255, 255, 255);
  outline: 0.15rem solid rgb(249, 87, 89);
  border: none;
  padding: 0.75rem;
  width: 12rem;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;
  font-weight: 200;
}

.option-left {
  border-radius: 1rem 0 0 1rem;
}
.option-right {
  border-radius: 0 1rem 1rem 0;
}

.option-active {
  background-color: rgb(249, 87, 89);
  color: rgb(255, 255, 255);
}


</style>