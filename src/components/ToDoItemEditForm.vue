<template>
  <!-- <form> listens for submit event. 
  Result: onSubmit() method is invoked, which checks to see if the new label value is not blank, and not the same as the old one
  , and if so emits the item-edited event (which is then listened for inside ToDoItem.vue, see above). -->
  <container_tag>
    <form class="stack-small" @submit.prevent="onSubmit">
        <div>
          <label class="edit-label">編輯 &quot;{{label}}&quot; 的名稱</label>
          <input :id="id" type="text" autocomplete="off" v-model.lazy.trim="newLabel" />
        </div>
        <div class="btn-group">
          <!-- "Cancel" <button> listens for click event. 
              Result: onCancel() method is invoked, which emits the edit-cancelled event (which is then listened for inside ToDoItem.vue, see above). -->
          <button type="button" class="btn btn__cancel" @click="onCancel">
              取消
              <span class="visually-hidden">editing {{label}}</span>
          </button>
          <button type="submit" class="btn btn__primary">
              儲存
              <span class="visually-hidden">edit for {{label}}</span>
          </button>
        </div>
    </form>
  </container_tag>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true
    },
    id: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      newLabel: this.label
    };
  },
  methods: {
    onSubmit() {
      if (this.newLabel && this.newLabel !== this.label) {
        this.$emit("item-edited", this.newLabel);
      }
    },
    onCancel() {
      this.$emit("edit-cancelled");
    }
  }
};
</script>
<style scoped>
.edit-label {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #0b0c0c;
  display: block;
  margin-bottom: 5px;
}
input {
  display: inline-block;
  margin-top: 0.4rem;
  width: 100%;
  min-height: 4.4rem;
  padding: 0.4rem 0.8rem;
  border: 2px solid #565656;
}
form {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
form > * {
  flex: 0 0 100%;
}
</style>