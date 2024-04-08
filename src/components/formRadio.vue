<template>
  <div class="form-radio">
    <label class="form-radio__label">{{label}}</label>
    <div class="form-radio__container">
      <div class="form-radio__box" v-for="(element, index) in elements" :key="index">
        <input class="custom-input" type="radio" :id="element.id" :name="name" :value="element" v-model="internalValue" />
        <label :for="element.id">{{ element }}</label>
      </div>
    </div>
    <span v-if="hasError" class="form-item__error">{{ errorMessage }}</span>
  </div>
</template>

<script>
export default {
  props: {
    elements: {
      type: Array,
      required: true
    },
    label : {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true
    },
    hasError: {
      type: Boolean,
      required: true
    },
    errorMessage: {
      type: String,
      default: 'Поле обязательно к заполнению'
    },
    value: {
      required: true
    },
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
.form-radio {
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;

  .form-radio__container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
  }

  .form-radio__box {
    font-size: 20px;
  }

  .form-radio__label {
    text-align: start;
    margin-bottom: 10px;
  }

  .form-item__error {
    padding-left: 10px;
    font-size: 12px;
    text-align: start;
    color: #f02630;
    margin-top: 4px;
  }
}

.custom-input {
  -webkit-appearance: none;
  appearance: none;
}

input[type="radio"].custom-input {
  border-radius: 50%;
}

.custom-input::before {
  display: block;
  content: "";
  width: 14px;
  height: 14px;
  transition: 120ms transform ease-in-out;
  box-shadow: inset 14px 14px #333;
}

input[type="radio"].custom-input::before {
  border-radius: 50%;
  transform: scale(0);
}

input[type="radio"].custom-input:checked::before {
  transform: scale(.7);
}

form {
  height: fit-content;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: auto;
  gap: 50px;
}

input, label {
  cursor: pointer;
}

input[type="radio"] {
  margin-right: 10px;
  transform: translateY(5px);
  width: 20px;
  height: 20px;
  border: 1px solid #333;
  padding: 2px;
}

h3 {
  text-transform: uppercase;
}

@media (max-width: 499px) {
  form {
    grid-template-columns: 1fr;
  }
}
</style>