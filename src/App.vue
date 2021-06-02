<template>
  <main id="todolist">
    <h1>
      Todo List
      <span>Get things done, one item at a time.</span>
    </h1>
    <template v-if="todo.length">
      <transition-group name="todolist" tag="ul">
        <Card
          v-for="item in todo"
          :item="item"
          v-bind:key="item.id"
          @mark-as-done="markAsDoneOrUndone"
          @delete-item="deleteItemFromList"
        />
      </transition-group>
    </template>

    <p v-else class="emptylist">Your todo list is empty.</p>

    <div class="newitem">
      <label for="newitem">Add to the todo list</label>
      <input
        type="text"
        name="newitem"
        v-model="newitem"
        @input="assertMaxChars()"
        autocomplete="off"
      />
      <button @click="addItem()">Add item</button>
    </div>
    <span>{{ limit }}/50</span>
  </main>
</template>

<script>
import Card from "./components/Card.vue";
export default {
  name: "App",
  components: {
    Card,
  },
  data() {
    return {
      newitem: "",
      todo: [],
      maxLengthInCars: 50,
    };
  },
  computed: {
    limit() {
      return this.newitem.length;
    },
  },
  methods: {
    addItem: function() {
      if (!this.newitem) return;

      this.todo.push({
        id: Math.floor(Math.random() * 9999) + 10,
        label: this.newitem,
        done: false,
      });
      this.newitem = "";
    },
    markAsDoneOrUndone: function(item) {
      item.done = !item.done;
    },
    deleteItemFromList: function(item) {
      let index = this.todo.indexOf(item);
      this.todo.splice(index, 1);
    },
    assertMaxChars: function() {
      if (this.newitem.length >= this.maxLengthInCars) {
        this.newitem = this.newitem.substring(0, this.maxLengthInCars);
      }
    },
  },
};
</script>

<style>
html CSS JS Result Skip Results iframe * {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html,
body {
  background: #f7f1f1;
  font-size: 1.1rem;
  font-family: "Quicksand", sans-serif;
  height: 100%;
}
@keyframes strikeitem {
  to {
    width: calc(100% + 1rem);
  }
}

#todolist {
  margin: 4rem auto;
  padding: 2rem 3rem 3rem;
  max-width: 500px;
  background: #43d6a5;
  color: #fff;
  box-shadow: -20px -20px 0px 0px rgba(100, 100, 100, 0.1);
}
#todolist h1 {
  /*text-align:center;*/
  font-weight: normal;
  font-size: 2.6rem;
  letter-spacing: 0.05em;
  border-bottom: 1px solid rgba(255, 255, 255, 0.3);
}
#todolist h1 span {
  display: block;
  font-size: 0.8rem;
  margin-bottom: 0.7rem;
  margin-left: 3px;
  margin-top: 0.2rem;
}

#todolist .emptylist {
  margin-top: 2.6rem;
  text-align: center;
  letter-spacing: 0.05em;
  font-style: italic;
  opacity: 0.8;
}
#todolist ul {
  margin-top: 2.6rem;
  list-style: none;
}
#todolist .todolist-move {
  transition: transform 1s;
}

/* add new items */
.newitem {
  margin-top: 3rem;
  display: flex;
  flex-wrap: wrap;
}
.newitem label {
  min-width: 100%;
  margin-bottom: 0.5rem;
  font-size: 1.3rem;
}
.newitem input {
  flex-grow: 1;
  border: none;
  background: #f7f1f1;
  padding: 0 1.5em;
  font-size: initial;
}
.newitem input:focus {
  outline: none;
}
.newitem button {
  padding: 0 1.3rem;
  border: none;
  background: #555555;
  color: white;
  text-transform: uppercase;
  font-weight: bold;
  /* border: 1px solid rgba(255, 255, 255, 0.3); */
  margin-left: 5px;
  cursor: pointer;
  transition: background 0.2s ease-out;
  font-size: 12px;
}
.newitem button:hover {
  background: #727272;
}
.newitem input,
.newitem button {
  font-family: "Quicksand", sans-serif;
  height: 3rem;
  border-radius: 0.3em;
}
</style>
