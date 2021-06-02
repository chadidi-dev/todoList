<template>
  <li v-bind:class="item.done ? 'done' : ''">
    <div style="display:flex;">
      <button
        class="btn-picto"
        type="button"
        v-on:click="markAsDoneOrUndone(item)"
        v-bind:aria-label="item.done ? 'Undone' : 'Done'"
        v-bind:title="item.done ? 'Undone' : 'Done'"
      >
        <i aria-hidden="true" class="material-icons">{{
          item.done ? "check_box" : "check_box_outline_blank"
        }}</i>
      </button>
      <span class="label">{{ item.label }}</span>
    </div>
    <button
      class="btn-picto"
      type="button"
      v-on:click="deleteItemFromList()"
      aria-label="Delete"
      title="Delete"
    >
      <i aria-hidden="true" class="material-icons">delete</i>
    </button>
  </li>
</template>

<script>
export default {
  props: ["item"],
  methods: {
    markAsDoneOrUndone: function(item) {
      this.$emit("mark-as-done", item);
    },
    deleteItemFromList: function() {
      this.$emit("delete-item");
    },
  },
};
</script>

<style scoped>
li {
  display: flex;
  flex-direction: row;
  margin: 0 -3rem 4px;
  padding: 1.1rem 1.5rem;
  justify-content: space-between;
  align-items: center;
  background: rgba(255, 255, 255, 0.1);
}

.actions {
  flex-shrink: 0;
  padding-left: 0.7em;
}
.label {
  position: relative;
  transition: opacity 0.2s linear;
}
.done .label {
  opacity: 0.6;
}
.done .label:before {
  content: "";
  position: absolute;
  top: 50%;
  left: -0.5rem;
  display: block;
  width: 0%;
  height: 1px;
  background: #fff;
  animation: strikeitem 0.3s ease-out 0s forwards;
}
.btn-picto {
  border: none;
  background: none;
  -webkit-appearance: none;
  cursor: pointer;
  color: #fff;
}
</style>
