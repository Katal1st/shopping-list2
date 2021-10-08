<template>
  <div class="todo-item">
    <div class="todo-item-left">
        <input type="checkbox" v-model="completed" @change="doneEdit">
        <div v-if="!editing" @dblclick="editTodo" class="todo-item-label" :class="{ completed : completed }">{{ title }}</div>
        <div v-if="!editing" @dblclick="editTodo" class="todo-item-label" :class="{ completed : completed }">quantity: {{ quantity }}</div>
        <div v-if="!editing" @dblclick="editTodo" class="todo-item-label" :class="{ completed : completed }">cost: {{ cost }}$</div>
        <div v-if="!editing" @dblclick="editTodo" class="todo-item-label" :class="{ completed : completed }">sum: {{ sum }}$</div>
        <input v-else class="todo-item-edit" type="text" v-model="title" @blur="doneEdit" @keyup.enter="doneEdit" @keyup.esc="cancelEdit" v-focus>
      </div>
      <div class="remove-item" @click="removeTodo(todo.id)">
        &times;
      </div>
  </div>
</template>

<script>
export default {
  name: 'todo-item',
  props: {
    todo: {
      type: Object,
      required: true,
    },
    checkAll: {
      type: Boolean,
      required: true,
    }
  },
  data() {
    return {
      'id': this.todo.id,
      'title': this.todo.title,
      'quantity': this.todo.quantity,
      'cost': this.todo.cost,
      'completed': this.todo.completed,
      'editing': this.todo.editing,
      'beforeEditCache': '',
    }
  },
  watch: {
    checkAll() {
      // if (this.checkAll) {
      //   this.completed = true
      // } else {
      //   this.completed = this.todo.completed
      // }
      this.completed = this.checkAll ? true : this.todo.completed
    }
  },
  directives: {
    focus: {
      inserted: function (el) {
        el.focus()
      }
    }
  },
  methods: {
    removeTodo(id) {
      this.$emit('removedTodo', id)
    },
    editTodo() {
      this.beforeEditCache = this.title
      this.beforeEditCache = this.quantity
      this.beforeEditCache = this.cost
      this.editing = true
    },
    doneEdit() {
      if (this.title.trim() == '') {
        this.title = this.beforeEditCache
      }
      this.editing = false
      this.$emit('finishedEdit', {
        'id': this.id,
        'title': this.title,
        'quantity': this.quantity,
        'cost': this.cost,
        'completed': this.completed,
        'editing': this.editing,
      })
    },
    cancelEdit() {
      this.title = this.beforeEditCache
      this.quantity = this.beforeEditCache
      this.cost = this.beforeEditCache
      this.editing = false
    },
  },
  computed: {
    sum() {
      return this.cost * this.quantity
    }
  }
}
</script>