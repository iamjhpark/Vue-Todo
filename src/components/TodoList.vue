<template>
  <div>
      <ul>
          <li v-for="(todoItem, index) in this.todoItems" v-bind:key="todoItem.item" class="shadow">
              <div class="checkBtn" v-bind:class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem, index)">*</div>
              <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
              <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
                  <div>-</div>
              </span>
          </li>
      </ul>
  </div>
</template>

<script>
import { mapGetters, mapMutations } from 'vuex';

export default {
    methods: {
        ...mapMutations([
            "removeOneItem",
            "toggleOneItem",
        ]),
        removeTodo(todoItem, index) {
            const payload = {
                todoItem,
                index,
            }
            this.removeOneItem(payload);
            // this.$store.commit("removeOneItem", payload);
        },
        toggleComplete(todoItem, index) {
            const payload = {
                todoItem,
                index,
            }
            this.toggleOneItem(payload);
            // this.$store.commit("toggleOneItem", payload);
        },
    },
    computed: {
        // ...mapGetters(["storedTodoItems"]),
        ...mapGetters({
            todoItems: "storedTodoItems",
        }),
    }
}
</script>

<style scoped>
ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
}
li {
    display: flex;
    min-height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9 rem;
    background: white;
    border-radius: 5px;
}
.checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
    cursor: pointer;
}
.checkBtnCompleted {
    color: #b3adad;
}
.textCompleted {
    text-decoration: line-through;
    color: #b3adad;
}
.removeBtn {
    margin-left: auto;
    color: #de4343;
    cursor: pointer;
}
</style>