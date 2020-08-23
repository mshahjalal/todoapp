<template>
  <div class="todo-list">
    <div class="new-input">
      <input type="text" id="todo-input-label" class="todo-input" placeholder="What needs to be done?" v-model="newTodo" @keyup.enter="addTodo">
      <label for="todo-input-label"></label>
    </div>
    

    <todo-item v-for="todo in todosFiltered" :key="todo.id" :todo="todo"></todo-item>

    <todo-filter></todo-filter>
  </div>
</template>

<script>
import TodoItem from './TodoItem'
import TodoFilter from './TodoFilter'
export default {
  name: 'todo-list',
  components: {
    TodoItem,
    TodoFilter
  },
  data () {
    return {
      newTodo: '',
      idForTodo: 1
    }
  },
  computed: {
    todosFiltered() {
      return this.$store.getters.todosFiltered
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length == 0) {
        return
      }
      this.$store.dispatch('addTodo', {
        id: this.idForTodo,
        title: this.newTodo,
      })
      this.newTodo = ''
      this.idForTodo++
    }
  }
}
</script>

<style lang="scss">
  h1 {
      margin: 0;
      width: 100%;
      font-size: 100px;
      font-weight: 100;
      text-align: center;
      color: #af2f2f;
      text-rendering: optimizeLegibility;
    }
    .new-input {
      position: relative;
      left: 0;
      top: 0;

      label {
        width: 60px;
        height: 34px;
        font-size: 0;
        position: absolute;
        top: 8px;
        left: -13px;
        -webkit-transform: rotate(90deg);
        transform: rotate(90deg);
      }
      .todo-input {
        width: 100%;
        font-size: 18px;
        padding: 16px 16px 16px 70px;
        border: none;
        background: rgba(0, 0, 0, 0.003);
        box-shadow: inset 0 -2px 1px rgba(0,0,0,0.03);
        &:focus {
          outline: 0;
        }
      }
  
      label:before {
          content: '❯';
          font-size: 22px;
          color: #e6e6e6;
          padding: 10px 27px 10px 27px;
      }
    }
  
  .todo-list {
    background: #fff !important;
    margin: 0px 0 10px 0;
    box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 2px 25px 25px 0 rgba(0, 0, 0, 0.1); 
  }
  .todo-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-top: 1px solid #ededed;
    width: 100%;

    .todo-item-checkbox {
        width:40px;
    }
    .todo-item-label {
      padding: 10px 0px 10px 15px;
      margin-left: 12px;
      border: 1px solid white;
      width: 100%;
    }
    .remove-item {
      font-size: 30px;
      color: #cc9a9a;
      padding: 0px 10px;
      width: 6.5%;
    }
    .todo-item-edit {
      margin-left: 12px;
      width: calc(100% - 40px);
      padding: 10px 0px 10px 10px;
      border: 1px solid #999;
      box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2);
      box-sizing: border-box;
      font-size: inherit;
      font-family: 'Avenir', Helvetica, Arial, sans-serif;

      &:focus {
        outline: none;
      }
    }
  }

  .completed {
    text-decoration: line-through;
    color: grey;
  }
  .extra-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 16px;
    border-top: 1px solid lightgrey;
    padding: 14px 0px;
    margin-bottom: 14px;

    .todo-remaining {
      width: 25%;
      padding-left: 12px;
    }
    .todo-filters {
      width: 52%;
    }
    .todo-clear-completed {
        width: 17.5%;
        margin-right: 12px;
    }
  }
  button {
      cursor: pointer;
      margin: 3px;
      padding: 3px 7px;
      text-decoration: none;
      border: 1px solid transparent;
      border-radius: none;     
      background: none;
      font-size: 14px;
      vertical-align: baseline;
      font-family: inherit;
      font-weight: inherit;
      color: inherit;
      -webkit-appearance: none;
      appearance: none;
      -webkit-font-smoothing: antialiased;
      line-height: 20px;


      &:focus {
        outline: none;
      }

      &:hover {
          border: 1px solid #cc9a9a;
          border-radius: 3px; 
      }
  }
  button.clear-completed {
      margin: 0px !important;
      padding: 0px !important;
      border: none !important;      
      border-radius: 0px !important;

      &:hover {
          text-decoration: underline !important;
      }
  }
  .todo-filters .active {
    border: 1px solid #cc9a9a;
    border-radius: 3px; 
  }


/* checkbox aspect */
[type="checkbox"]:not(:checked):before,
[type="checkbox"]:checked:before {
  content: '';
  position: absolute;
  left: 4px; 
  top: -5px;
  width: 1.65em;
  height: 1.65em;
  border: 1px solid #ccc;
  background: #fff;
  border-radius: 30px;
  box-shadow: inset 0 1px 3px rgba(0,0,0,.1);
}
/* checked mark aspect */
[type="checkbox"]:checked:after {
  content: '\2713\0020';
  position: absolute;
  top: .05em; 
  left: .6em;
  font-size: 1.3em;
  line-height: 0.8;
  color: #09ad7e;
  transition: all .2s;
  font-family: 'Lucida Sans Unicode', 'Arial Unicode MS', Arial;
}
/* checked mark aspect changes */
[type="checkbox"]:not(:checked) {
  opacity: 1;
  transform: scale(1);
}
[type="checkbox"]:checked {
  opacity: 1;
  transform: scale(1);
}

</style>