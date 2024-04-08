<template>
  <form @submit.prevent="submitForm" class="form">
    <div class="form-container">
      <div class="form-section">
        <h3 class="form-title">Атрибуты</h3>
        <form-item
            label="Фамилия*"
            :value="formData.lastName"
            :hasError="v$.lastName.$error"
            :errorMessage="v$.lastName.$errorMessage"
            @input="formData.lastName = $event"
        ></form-item>

        <form-item
            label="Имя*"
            :value="formData.firstName"
            :hasError="v$.firstName.$error"
            :errorMessage="v$.firstName.$errorMessage"
            @input="formData.firstName = $event"
        ></form-item>

        <form-item
            label="Отчество*"
            :value="formData.surName"
            :hasError="v$.surName.$error"
            :errorMessage="v$.surName.$errorMessage"
            @input="formData.surName = $event"
        ></form-item>

        <form-item
            label="Дата рождения"
            :value="formData.dateBirth"
            :hasError="v$.dateBirth.$error"
            :errorMessage="v$.dateBirth.$errorMessage"
            newType = "datetime-local"
            @input="formData.dateBirth = $event"
        ></form-item>

        <form-item
            label="Номер телефона*"
            :value="formData.numberPhone"
            :hasError="v$.numberPhone.$error"
            :errorMessage="v$.numberPhone.$errors.length > 0 ? 'Номер введен некорректно' : v$.numberPhone.$errorMessage"
            @input="formData.numberPhone = $event"
        ></form-item>

        <form-radio
            label="Пол"
            :value="formData.sex"
            :elements="sexArr"
            :hasError="v$.sex.$error"
            :errorMessage="v$.sex.$errorMessage"
            name="sex"
            @input="formData.sex = $event"
        ></form-radio>

        <form-select
            label="Группа клиентов*"
            :options="clientGroups"
            :hasError="v$.clientGroups.$error"
            :errorMessage="v$.clientGroups.$errorMessage"
            @input="formData.clientGroups = $event"
        ></form-select>

        <form-select
            label="Группа клиентов*"
            :type=false
            :options="doctors"
            :hasError="v$.attendingDoctor.$error"
            :errorMessage="v$.attendingDoctor.$errorMessage"
            @input="formData.attendingDoctor = $event"
        ></form-select>

        <FormCheckbox
            :elements="sms"
            :value="formData.sms"
            :hasError="v$.sms.$error"
            :errorMessage=v$.sms.$errorMessage
            @input="formData.sms = $event"
        />
      </div>
      <div class="form-section">
        <h3 class="form-title">Адрес</h3>
        <form-item
            label="Индекс"
            :value="formData.index"
            :hasError="v$.index.$error"
            :errorMessage="v$.index.$errorMessage"
            @input="formData.index = $event"
        ></form-item>

        <form-item
            label="Страна"
            :value="formData.country"
            :hasError="v$.country.$error"
            :errorMessage="v$.country.$errorMessage"
            @input="formData.country = $event"
        ></form-item>

        <form-item
            label="Область"
            :value="formData.region"
            :hasError="v$.region.$error"
            :errorMessage="v$.region.$errorMessage"
            @input="formData.region = $event"
        ></form-item>

        <form-item
            label="Город*"
            :value="formData.city"
            :hasError="v$.city.$error"
            :errorMessage="v$.city.$errorMessage"
            @input="formData.city = $event"
        ></form-item>

        <form-item
            label="Улица"
            :value="formData.street"
            :hasError="v$.street.$error"
            :errorMessage="v$.street.$errorMessage"
            @input="formData.street = $event"
        ></form-item>

        <form-item
            label="Дом"
            :value="formData.house"
            :hasError="v$.house.$error"
            :errorMessage="v$.house.$errorMessage"
            @input="formData.house = $event"
        ></form-item>
      </div>
      <div>
        <h3 class="form-title">Паспорт</h3>
        <form-select
            label="Тип документа*"
            :type=false
            :options="documentType"
            :hasError="v$.documentType.$error"
            :errorMessage="v$.documentType.$errorMessage"
            @input="formData.documentType = $event"
        ></form-select>

        <form-item
            label="Серия"
            :value="formData.series"
            :hasError="v$.series.$error"
            :errorMessage="v$.series.$errorMessage"
            @input="formData.series = $event"
        ></form-item>

        <form-item
            label="Номер"
            :value="formData.number"
            :hasError="v$.number.$error"
            :errorMessage="v$.number.$errorMessage"
            @input="formData.number = $event"
        ></form-item>

        <form-item
            label="Кем выдан"
            :value="formData.issuedBy"
            :hasError="v$.issuedBy.$error"
            :errorMessage="v$.issuedBy.$errorMessage"
            @input="formData.issuedBy = $event"
        ></form-item>

        <form-item
            label="Дата выдачи*"
            :value="formData.dateIssue"
            newType = "datetime-local"
            :hasError="v$.dateIssue.$error"
            :errorMessage="v$.dateIssue.$errorMessage"
            @input="formData.dateIssue = $event"
        ></form-item>
      </div>
    </div>

    <button class="form-button" type="submit">Отправить</button>
  </form>
</template>

<script setup>
import { reactive } from 'vue'
import { useVuelidate } from '@vuelidate/core'
import {helpers, required} from '@vuelidate/validators'
import FormItem from "@/components/formItem.vue";
import FormRadio from "@/components/formRadio.vue";
import FormSelect from "@/components/formSelect.vue";
import FormCheckbox from "@/components/formCheckbox.vue";

const sexArr = ["men", "women"]
const sms = [{ label: "Не отправлять", value: true }];
const clientGroups = [
  { label: 'VIP', value: 'VIP' },
  { label: 'Проблемные', value: 'Проблемные' },
  { label: 'ОМС', value: 'ОМС' }
];

const documentType = [
  { label: 'Паспорт', value: 'Паспорт' },
  { label: 'Свидетельство о рождении ', value: 'Свидетельство о рождении ' },
  { label: 'Вод. удостоверение', value: 'Вод. удостоверение' }
];

const doctors = [
  { label: 'Иванов', value: 'Иванов'},
  { label: 'Захаров', value: 'Захаров'},
  { label: 'Чернышева', value: 'Чернышева'}
];

const phoneValidation = helpers.regex(/^7\d{10}$/);

const formData = reactive({
  firstName: '',
  lastName: '',
  surName: '',
  dateBirth: '',
  numberPhone:'',
  sex: '',
  clientGroups: [],
  attendingDoctor: '',
  sms: [],
  index: '',
  country: '',
  region: '',
  city: '',
  street: '',
  house: '',
  documentType: '',
  series: '',
  number: '',
  issuedBy: '',
  dateIssue: '',
});

const rules = {
  firstName: { required },
  lastName: { required },
  surName: {},
  dateBirth: { required },
  numberPhone: { required, phoneValidation },
  sex: {required},
  clientGroups: { required },
  attendingDoctor: {},
  sms: {},
  index: {},
  country: {},
  region: {},
  city:{ required },
  street: {},
  house:{},
  documentType:{ required },
  series: {},
  number: {},
  issuedBy: {},
  dateIssue: { required },
}


const v$ = useVuelidate(rules, formData);

const submitForm = async () => {
  const result = await v$.value.$validate();
  if (result) {
    alert("success, form submitted")
  } else {
    console.log(formData)
  }
}
</script>

<style>
.form {
  flex-direction: column;
  padding: 24px;
  box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.3);
  border-radius: 16px;
  margin: 0 24px;
  display: flex;
  align-items: end;

  .form-container {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;

    .form-section {
      margin-right: 24px;
    }

    .form-title {
      margin-bottom: 12px;
      text-align: start;
      text-transform: uppercase;
    }
  }

  .form-button {
    padding: 10px;
    font-size: 15px;
    background: #4287f5;
    border: none;
    color: #ffffff;
    border-radius: 10px;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.3s;
  }

  .form-button:hover {
    background-color: #3366cc;
  }

  .form-button:active {
    transform: scale(0.95);
  }
}

@media screen and (max-width: 600px) {
  .form-section {
    margin-bottom: 14px;
  }
}
</style>