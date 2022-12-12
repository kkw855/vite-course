<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
export default {
  data() {
    return {
      header: "Shopping List App",
      newItem: "",
      newItemHighPriority: false,
      editing: false,
      items: [
        { id: 1, label: "10 party hats", purchased: true, highPriority: false },
        { id: 2, label: "2 board games", purchased: true, highPriority: false },
        { id: 3, label: "20 cups", purchased: false, highPriority: true }
      ]
    };
  },
  computed: {
    reversedItems() {
      return [...this.items].reverse()
    }
  },
  methods: {
    saveItem() {
      this.items.push(
        {
          id: this.items.length + 1,
          label: this.newItem,
          purchased: false,
          highPriority: this.newItemHighPriority
        });
      this.newItem = "";
      this.newItemHighPriority = false
    },
    doEditing(editing) {
      this.editing = editing;
      this.newItem = "";
      this.newItemHighPriority = false
    },
    togglePurchased(item) {
      item.purchased = !item.purchased;
    }
  }
};
</script>

<template>
  <div id="shopping-list">
    <div class="header">
      <h1>{{ header || "Welcome" }}</h1>
      <button v-if="editing" class="btn btn-cancel" @click="doEditing(false)">Cancel</button>
      <button v-else class="btn btn-primary" @click="doEditing(true)">Add Item</button>
    </div>

    <div v-if="editing" class="add-item-form">
      <input
        v-model="newItem" type="text" placeholder="Add an item"
        @keyup.enter="saveItem" />
      <label>
        <input v-model="newItemHighPriority" type="checkbox" />
        High Priority
      </label>
      <button :disabled="newItem.length < 5" class="btn btn-primary" @click="saveItem">
        Save Item
      </button>
    </div>

    <p v-if="items.length === 0">Nice job! You've bought all your items!</p>
    <ul>
      <li
        v-for="item in reversedItems"
        :key="item.id" :class="{strikeout: item.purchased, priority: item.highPriority}"
        class="static-class" @click="togglePurchased(item)">
        {{ item.label }}
      </li>
    </ul>
  </div>
</template>

<style scoped>
body {
  background: #eff8ff;
  height: 100vh;
  width: 100vw;
  font-family: system-ui, BlinkMacSystemFont, -apple-system, Segoe UI, Roboto,
  Oxygen, Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 0;
}

.counter {
  font-size: 0.8rem;
  padding-left: 10px;
  padding-right: 10px;
}

#shopping-list {
  background: #fff;
  padding: 2rem;
  margin: 1rem;
  border-radius: 3px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.12), 0 2px 4px 0 rgba(0, 0, 0, 0.08);
  width: 95%;
  max-width: 900px;
}

h1 {
  color: #3d4852;
}

ul {
  list-style: none;
  padding: 0;
}

a {
  color: #6cb2eb;
  font-size: 1.25rem;
  transition: all 0.1s ease-in;
  margin-top: 0.5rem;
  display: block;
}

a:hover {
  color: #3490dc;
}

li,
p {
  display: flex;
  align-items: center;
  line-height: 1.75;
  letter-spacing: 0.5px;
  color: #3d4852;
  font-size: 1.25rem;
  cursor: pointer;
  transition: all 0.1s ease-in;
}

li:hover {
  color: #22292f;
}

li input {
  margin: 0 0.5rem 0;
}

#shopping-list > input,
#shopping-list > select {
  width: 100%;
  border-radius: 3px;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
  border: 1px solid #f1f5f8;
  color: #606f7b;
  padding: 0.5rem 0.75rem;
  box-sizing: border-box;
  font-size: 1rem;
  letter-spacing: 0.5px;
  margin: 0.5rem 0;
}

.add-item-form,
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.add-item-form input {
  width: 70%;
  border-radius: 3px;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
  border: 1px solid #f1f5f8;
  color: #606f7b;
  padding: 0.5rem 0.75rem;
  box-sizing: border-box;
  font-size: 1rem;
  letter-spacing: 0.5px;
  margin: 0.5rem 0;
}

.btn {
  border: none;
  border-radius: 3px;
  margin: auto 0;
  padding: 0.5rem 0.75rem;
  flex-shrink: 0;
  cursor: pointer;
  font-size: 0.9rem;
  letter-spacing: 0.5px;
  transition: all 0.1s ease-in;
}

.btn[disabled] {
  background: #8795a1;
}

.btn[disabled]:hover {
  background: #606f7b;
}

.btn-primary {
  background: #6cb2eb;
  color: #fff;
}

.btn-primary:hover {
  background: #3490dc;
}

.btn-cancel {
  background: #ef5753;
  color: #fff;
}

.btn-cancel:hover {
  background: #e3342f;
  color: #fff;
}

.strikeout {
  text-decoration: line-through;
  color: #b8c2cc;
}

.strikeout:hover {
  color: #8795a1;
}

.priority {
  color: #de751f;
}

input[type="checkbox"] {
  display: inline !important;
  box-shadow: none;
  width: auto;
}
</style>
