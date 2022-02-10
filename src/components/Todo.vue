<template>
  <div
    class="w-full border-l-4 py-5 px-4 flex items-center hover:bg-gray-100 cursor-pointer"
    :class="{
      'border-yellow-500': !todo.done,
      'border-green-400': todo.done,
    }"
  >
    <div
      class="w-2 h-2 rounded-xl mr-5"
      :class="{
        'bg-yellow-500': !todo.done,
        'bg-green-400': todo.done,
      }"
    ></div>
    <div>
      <h3>{{ todo.title }}</h3>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    todo: {
      type: Object,
      require: true,
    },
  },
};
</script>
