<template>
  <div class="multi-item">
    <label class="multi-item__label">{{ label }}</label>
    <select class="multi-item__select" :multiple="type" v-model="internalValue">
      <option v-for="(option, index) in options" :key="index" :value="option.value">{{ option.label }}</option>
    </select>
    <span v-if="hasError" class="error-message">{{ errorMessage }}</span>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true
    },
    type: {
      type: Boolean,
      default: true
    },
    options: {
      type: Array,
      required: true
    },
    value: {
      type: Array,
      default: () => []
    },
    hasError: {
      type: Boolean,
      default: false
    },
    errorMessage: {
      type: String,
      default: 'Поле обязательно к заполнению'
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
.multi-item {
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;

  .multi-item__label {
    font-size: 14px;
    margin-bottom: 10px;
    text-align: start;
  }

  .multi-item__select {
    height: 37px;
    padding: 10px;
    border: none;
    border-radius: 5px;
    box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.1);
    outline: 1px solid  #ccc;
  }

  .error-message {
    padding-left: 10px;
    font-size: 12px;
    text-align: start;
    color: #f02630;
    margin-top: 4px;
  }
}
</style>