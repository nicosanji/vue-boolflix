<template>
  <div class="input-group justify-content-end w-25 pe-3">
    <input
      type="text"
      class="form-control"
      v-model="query"
      @keyup.enter="$emit('search', query)"
      placeholder="Search show..."
    />
  </div>
</template>

<script>
export default {
  name: "SearchInput",
  data() {
    return {
      query: "",
    };
  },
};
</script>
