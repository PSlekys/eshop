<template>
  <div class="search">
    <div class="field">
      <div class="control">
        <input
          class="input"
          v-model="query"
          type="search"
          placeholder="Search..."
          v-on:keyup="callParent"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      query: "",
    };
  },
  methods: {
    callParent() {
      this.$emit("search", this.query);
    },
  },
};
</script>

<style scoped>
.field {
  margin-bottom: 1.5em;
}
</style>
