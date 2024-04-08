<template>
  <div class="form-item">
    <label class="form-item__label">{{ label }}</label>
    <input class="form-item__input" v-model="internalValue" :type="newType">
    <span v-if="hasError" class="form-item__error">{{ errorMessage }}</span>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true
    },
    value: {
      required: true
    },
    errorMessage: {
      type: String,
      default: 'Поле обязательно к заполнению'
    },
    hasError: {
      type: Boolean,
      required: true
    },
    newType: {
      type: String,
      default: "text"
    }
  },
  computed: {
    internalValue: {
      get() {
        return this.value;
      },
      set(newValue) {
        this.$emit('input', newValue);
      }
    }
  }
};
</script>

<style scoped>
.form-item {
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;

  .form-item__label {
    text-align: start;
    margin-bottom: 10px;
  }

  .form-item__input {
    padding: 10px;
    border: none;
    border-radius: 5px;
    box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.1);
    outline: 1px solid  #ccc;
    height: 37px;
  }

  .form-item__error {
    padding-left: 10px;
    font-size: 12px;
    text-align: start;
    color: #f02630;
    margin-top: 4px;
  }
}
</style>