<template>
    <div>
        <h1>Accessible Form validation!</h1>
    </div>
    <div>
        <form @submit.prevent="submitForm" ref="form">
        <div class="form-group">
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="name" :aria-invalid="nameError ? 'true' : 'false'" aria-describedby="name-error">
        <div v-if="nameError" class="error-message" id="name-error">{{ nameError }}</div>
        </div>
        <div class="form-group">
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="email" :aria-invalid="emailError ? 'true' : 'false'" aria-describedby="email-error">
        <div v-if="emailError" class="error-message" id="email-error">{{ emailError }}</div>
        </div>
        <button type="submit">Submit</button>
    </form>
    </div>
</template>
<script>
export default{
    data() {
        return {
            name: '',
            email: '',
            nameError: '',
            emailError: ''
        }
    },
    methods: {
      submitForm() {
        this.validateName();
        this.validateEmail();
        
        if (this.nameError || this.emailError) {
          this.focusOnErrorField();
        } else {
          alert('Form submitted successfully!');
          // Here you can perform further actions like submitting the form via AJAX
        }
      },
      validateName() {
        if (!this.name.trim()) {
          this.nameError = 'Please enter your name';
        } else {
          this.nameError = '';
        }
      },
      validateEmail() {
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (!this.email.trim()) {
          this.emailError = 'Please enter an email';
        } else if (!emailRegex.test(this.email)) {
          this.emailError = 'Invalid email format';
        } else {
          this.emailError = '';
        }
      },
      focusOnErrorField() {
        // Focus on the first field with an error
        if (this.nameError) {
          this.$refs.form.querySelector('#name').focus();
        } else if (this.emailError) {
          this.$refs.form.querySelector('#email').focus();
        }
      }
    }
}
 
</script>
<style scoped>
.form-group {
  margin-bottom: 20px;
}
.error-message {
  color: red;
  margin-top: 5px;
}
</style>