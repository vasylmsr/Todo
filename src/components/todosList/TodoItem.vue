<template>
  <base-card class="todo">
    <div>
      <div class="todo__title">{{todo.title}}</div>
      <div class="todo__author">by {{todo.author}}</div>
    </div>

    <div class="todo__controls">
      <checkbox-field
        :value="todo.done"
        @input="handleCheckboxClick"
      >
        {{todo.done ? 'Done' : 'Undone'}}
      </checkbox-field>

      <div class="todo__edit-buttons">
        <base-button type="danger" @click="$emit('delete', todo)">
          Delete
        </base-button>
        <base-button type="success" @click="$emit('view', todo)">
          View todo
        </base-button>
      </div>
    </div>
  </base-card>
</template>

<script>
import BaseButton from "../UI/BaseButton";
import CheckboxField from "@/components/UI/checkbox/CheckboxField";
import BaseCard from "../UI/BaseCard";

export default {
  name: "TodoItem",
  components: {
    BaseCard,
    CheckboxField,
    BaseButton,
  },
  props: {
    todo: {
      required: true,
      type: Object
    }
  },
  methods: {
    handleCheckboxClick(done) {
      this.$emit('edit', {...this.todo, done});
    },
  },
}
</script>

<style scoped lang="scss">
  .todo {
    display: flex;
    flex-direction: column;
    word-break: break-all;

    &__title {
      font-size: 18px;
      line-height: 1.2;
      font-weight: 600;
      margin-bottom: 5px;
    }

    &__author {
      font-style: italic;
      margin-bottom: 10px;
    }

    &__edit-buttons {
      display: grid;
      grid-template-columns: max-content max-content max-content;
      grid-gap: 10px;
      margin-top: 15px;
    }

    &__view-btn {
      margin-top: 10px;
    }

    &__title {
      word-break: break-all;

      &--done {
        text-decoration: line-through;
      }
    }

    &__controls {
      padding-top: 15px;
      margin-top: auto;
    }
  }

  .todo__text-wrapper {
    display: flex;
    align-items: center;
    margin-right: 5px;
  }

</style>
