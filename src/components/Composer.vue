<template>
  <form @submit.prevent="$emit('onAddTodo')">
    <input
      type="text"
      class="bg-gray-100 w-full focus:outline-none py-5 px-4 border-t-2 border-indigo-600"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
    />
  </form>
</template>

<script>
export default {
  props: ["modelValue"],
  emit: ["update:modelValue",'onAddTodo'],
};
</script>
