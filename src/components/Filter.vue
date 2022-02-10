<template>
  <div class="flex justify-between my-3">
    <div class="category flex justify-between w-52">
      <button
        @click="$emit('onFiltered', 'all')"
        :class="{
          'text-blue-300': filterMode === 'all',
        }"
      >
        All({{ allTodo }})
      </button>
      <button @click="$emit('onFiltered', 'pending')"
      :class="{
          'text-blue-300': filterMode === 'pending',
        }"
      >
        Pending({{ pendingTodo }})
      </button>
      <button @click="$emit('onFiltered', 'done')"
      :class="{
          'text-blue-300': filterMode === 'done',
        }"
      >Done({{ doneTodo }})</button>
    </div>
    <div class="clear">
      <button @click="$emit('onDdeleteTodos')" class="text-red-500">Clear</button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    allTodo: {
      type: Number,
      require: true,
    },
    pendingTodo: {
      type: Number,
      require: true,
    },
    doneTodo: {
      type: Number,
      require: true,
    },
    filterMode: {
      type: String,
    },
  },
  emit: ["onDdeleteTodos", "onFiltered"],
};
</script>
