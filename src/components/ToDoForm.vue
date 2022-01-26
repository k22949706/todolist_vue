<template>
  <!-- <form> listens for submit event. Result: onSubmit() method is invoked, which checks that the new label is not empty
      , then emits the todo-added event (which is then listened for inside App.vue, see above), and finally clears the new label <input>. -->
  <form @submit.prevent="onSubmit">
    <h2 class="label-wrapper">
    <label for="new-todo-input" class="label__lg">
        新增任務:
    </label>
    </h2>
    <div class="flex">
        <input
            type="text"
            id="new-todo-input"
            name="new-todo"
            autocomplete="off"
            v-model.lazy.trim="label"
            class="input__lg"
        />
        <button type="submit" class="btn btn__primary">
            新增
        </button>
    </div>
  </form>
</template>

<script>
  export default {
    methods: {
       onSubmit() {
          if(this.label === "") {
              return;
          }
          this.$emit('todo-added', this.label);
          this.label = "";
       }
    },
    data() {
        return {
            label: ""
        };
    }
  };
</script>