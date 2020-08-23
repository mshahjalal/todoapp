<template>
    <div class="extra-container" v-if="anyCompleted || anyRemaining">
      <div class="todo-remaining">{{ remaining }} {{remainingItemText}}</div>
      <div class="todo-filters">
        <button :class="{ active: filter == 'all' }" @click="changeFilter('all')">All</button>
        <button :class="{ active: filter == 'active' }" @click="changeFilter('active')">Active</button>
        <button :class="{ active: filter == 'completed' }" @click="changeFilter('completed')">Completed</button>
      </div>

      <div class="todo-clear-completed">
        <button v-if="showClearCompletedButton" @click="clearCompleted" class="clear-completed">Clear completed</button>
      </div>
    </div>
</template>

<script>
export default {
  name: 'todo-filter',
  computed: {
    filter() {
      return this.$store.state.filter
    },
    remaining() {
      return this.$store.getters.remaining
    },
    anyRemaining() {
      return this.$store.getters.anyRemaining
    },
    anyCompleted() {
        return this.$store.getters.anyCompleted
    },
    showClearCompletedButton() {
      return this.$store.getters.anyCompleted
    },
    remainingItemText() {
        return this.$store.getters.remaining > 1 ? " items left" : " item left"
    }
  },
  methods: {
    changeFilter(filter) {
      this.$store.dispatch('updateFilter', filter)
    },
    clearCompleted() {
      this.$store.dispatch('clearCompleted')
    }
  }
}
</script>