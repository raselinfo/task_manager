<template>
  <div
    class="w-96 p-5 fixed bottom-0 right-5 rounded-md mb-5"
    :class="{
      'bg-red-400': message.error.length > 0,
      'bg-green-500': message.success.length > 0,
    }"
  >
    <h4>{{ message.success }}{{ message.error }}</h4>
  </div>
</template>
<script>
export default {
  props: {
    message: {
      type: Object,
    },
  },
};
</script>
