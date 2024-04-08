<template>
  <div class="form-checkbox">
    <div class="form-checkbox__container">
      <div class="form-group" v-for="(element, index) in elements" :key="index">
        <input class="custom-input" type="checkbox" :id="element.id" :value="element.value" :checked="isChecked(element.value)" @change="updateValue($event.target.value, $event.target.checked)" />
        <label  :for="element.id">{{ element.label }}</label>
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
    value: {
      type: Array,
      required: true
    },
    hasError: {
      type: Boolean,
      required: true
    },
    errorMessage: {
      type: String,
      default: 'Поле обязательно к заполнению'
    }
  },
  methods: {
    isChecked(val) {
      return this.value.includes(val);
    },
    updateValue(val, checked) {
      if (checked) {
        this.$emit('input', [...this.value, val]);
      } else {
        this.$emit('input', this.value.filter(item => item !== val));
      }
    }
  }
};
</script>

<style scoped>
.form-checkbox {
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;

  .form-checkbox__container {
    display: flex;
    flex-direction: row;
    align-items: center;
  }

  .form-item__error {
    padding-left: 10px;
    font-size: 12px;
    text-align: start;
    color: #f02630;
    margin-top: 6px;
  }

  .custom-input {
    -webkit-appearance: none;
    appearance: none;
  }

  input[type="checkbox"].custom-input {
    border-radius: 3px;
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

  input[type="checkbox"].custom-input::before {
    transform-origin: bottom left;
    clip-path: polygon(14% 44%, 0 65%, 50% 100%, 100% 16%, 80% 0%, 43% 62%);
    transform: scale(0);
  }

  input[type="checkbox"].custom-input:checked::before{
    transform: scale(1);
  }

  input[type="radio"].custom-input::before {
    border-radius: 50%;
    transform: scale(0);
  }

  input[type="radio"].custom-input:checked::before {
    transform: scale(.7);
  }

  body {
    padding: 5rem 10vw;
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

  @media (max-width: 499px) {
    form {
      grid-template-columns: 1fr;
    }
  }

  .form-group {
    font-size: 14px;
  }

  input[type="checkbox"], input[type="radio"] {
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

  p {
    font-size: 20px;
  }

  code {
    background: linear-gradient(to top, yellow 20%, #0000 80%);
    font-size: 16px;
  }
}
</style>