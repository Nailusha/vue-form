<template>
  <div class="form-container">
    <form @submit.prevent="submitForm">
      <h2>Форма создания Клиента</h2>
      <div class="form-group">
        <label for="last-name">Фамилия*</label>
        <input type="text" id="last-name" v-model.trim="formData.lastName" required>
        <span v-if="!$v.formData.lastName.required">Поле 'Фамилия' обязательно для заполнения</span>
      </div>

      <!-- Поле Имя -->
      <div class="form-group">
        <label for="first-name">Имя*</label>
        <input type="text" id="first-name" v-model.trim="formData.firstName" required>
        <span v-if="!$v.formData.firstName.required">Поле 'Имя' обязательно для заполнения</span>
      </div>

      <!-- Поле Отчество -->
      <div class="form-group">
        <label for="middle-name">Отчество</label>
        <input type="text" id="middle-name" v-model.trim="formData.middleName">
      </div>

      <!-- Поле Дата рождения -->
      <div class="form-group">
        <label for="birthdate">Дата рождения*</label>
        <input type="date" id="birthdate" v-model="formData.birthdate" required>
        <span v-if="!$v.formData.birthdate.required">Поле 'Дата рождения' обязательно для заполнения</span>
      </div>

      <!-- Поле Номер телефона -->
      <div class="form-group">
        <label for="phone">Номер телефона*</label>
        <input type="tel" id="phone" v-model.trim="formData.phone" pattern="7[0-9]{10}" required>
        <span v-if="!$v.formData.phone.required">Поле 'Номер телефона' обязательно для заполнения</span>
        <span v-if="!$v.formData.phone.pattern">Номер телефона должен начинаться с '7' и содержать 11 цифр</span>
      </div>

      <!-- Остальные поля формы -->

      <button type="submit">Создать клиента</button>
      <p v-if="formSubmitted">Новый клиент успешно создан!</p>
    </form>
  </div>
</template>

<script>
import { validationMixin } from 'vuelidate';

export default {
  mixins: [validationMixin],
  data() {
    return {
      formData: {
        lastName: '',
        firstName: '',
        middleName: '',
        birthdate: '',
        phone: '',
        // Добавьте остальные поля формы
      },
      formSubmitted: false
    };
  },
  validations: {
    formData: {
      lastName: {
        required: (value) => !!value.trim()
      },
      firstName: {
        required: (value) => !!value.trim()
      },
      birthdate: {
        required: (value) => !!value
      },
      phone: {
        required: (value) => !!value,
        pattern: (value) => /^7\d{10}$/.test(value)
      },
      // Добавьте валидацию для остальных полей формы
    }
  },
  methods: {
    submitForm() {
      this.$v.$touch();
      if (!this.$v.$invalid) {
        // Ваш код для отправки данных формы
        this.formSubmitted = true;
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.form-container {
  max-width: 600px;
  margin: 0 auto;
}

.form-group {
  margin-bottom: 20px;

  label {
    display: block;
    font-weight: bold;
  }

  input {
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
  }

  span {
    color: red;
  }
}

button {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

p {
  margin-top: 10px;
  color: green;
}
</style>
